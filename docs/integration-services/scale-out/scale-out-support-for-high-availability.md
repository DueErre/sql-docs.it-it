---
title: "Supporto della disponibilità elevata in SQL Server Integration Services (SSIS) Scale Out | Microsoft Docs"
ms.description: This article describes how to configure SSIS Scale Out for high availability
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 906edbe80e7c762cdd9a271218d790edc9da8f5b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="scale-out-support-for-high-availability"></a>Supporto della disponibilità elevata in Scale Out

In SSIS Scale Out la disponibilità elevata sul lato Scale Out Worker viene assicurata attraverso l'esecuzione di pacchetti con più istanze di Scale Out Worker.

La disponibilità elevata sul lato Scale Out Master è invece garantita dalla soluzione [Always On per il catalogo SSIS](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) e dal servizio clustering di failover di Windows. In questa soluzione più istanze di Scale Out Master sono ospitate in un cluster di failover di Windows. Quando il servizio Scale Out Master o il database SSISDB è inattivo nel nodo primario, il servizio o il database SSISDB nel nodo secondario continua ad accettare le richieste degli utenti e a comunicare con le istanze di Scale Out Worker. 

Per configurare la disponibilità elevata sul lato Scale Out Master, eseguire le operazioni seguenti:

## <a name="1-prerequisites"></a>1. Prerequisites
Configurare un cluster di failover di Windows Vedere il post di blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Installazione della funzionalità di clustering di failover e degli strumenti per Windows Server 2012) per le istruzioni. Installare la funzionalità e gli strumenti in tutti i nodi del cluster.

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2. Installare Scale Out Master nel nodo primario
Installare i servizi del motore di database di SQL Server, Integration Services e Scale Out Master nel nodo primario per Scale Out Master. 

Durante l'installazione, eseguire le operazioni seguenti:

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Impostare l'account che esegue il servizio Scale Out Master su un account di dominio
Questo account dovrà poi poter accedere al database SSISDB nel nodo secondario nel cluster di failover di Windows. Poiché il failover del servizio Scale Out Master e del database SSISDB può essere eseguito separatamente, questi due componenti possono anche non trovarsi nello stesso nodo dopo il failover.

![Configurazione del server a disponibilità elevata](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 Includere il nome host DNS del servizio Scale Out Master nei nomi comuni (CN) del certificato di Scale Out Master

Questo nome host viene usato nell'endpoint di Scale Out Master. 

![Configurazione del master a disponibilità elevata](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3. Installare Scale Out Master nel nodo secondario
Installare i servizi del motore di database di SQL Server, Integration Services e Scale Out Master nel nodo secondario per Scale Out Master. 

Usare lo stesso certificato di Scale Out Master applicato nel nodo primario. Esportare il certificato SSL di Scale Out Master presente nel nodo primario con una chiave privata e installarlo nell'archivio radice dei certificati del computer locale nel nodo secondario. Selezionare questo certificato durante l'installazione di Scale Out Master nel nodo secondario.

![Configurazione del master a disponibilità elevata 2](media/ha-master-config2.PNG)

> [!NOTE]
> È possibile configurare più istanze di backup di Scale Out Master ripetendo queste operazioni per Scale Out Master in altri nodi secondari.

## <a name="4-set-up-ssisdb-always-on"></a>4. Configurare la funzionalità Always On per il database SSISDB

Seguire le istruzioni per configurare Always On per il database SSISDB disponibili in [Always On per il catalogo SSIS (SSISDB)](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

È anche necessario creare un listener del gruppo di disponibilità per il gruppo di disponibilità in cui viene aggiunto il database SSISDB. Vedere [Creare o configurare un listener del gruppo di disponibilità](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5. Aggiornare il file di configurazione del servizio Scale Out Master
Aggiornare il file di configurazione del servizio Scale Out Master `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config` nel nodo master e secondario. Aggiornare **SqlServerName** in *[Nome DNS del listener del gruppo di disponibilità],[Porta]*.

## <a name="6-enable-package-execution-logging"></a>6. Abilitare la registrazione dell'esecuzione dei pacchetti

La registrazione nel database SSISDB viene eseguita dall'account di accesso **##MS_SSISLogDBWorkerAgentLogin##** la cui password viene generata automaticamente. Per il corretto funzionamento della registrazione per tutte le repliche del database SSISDB, eseguire le operazioni seguenti

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 Modificare la password di **##MS_SSISLogDBWorkerAgentLogin##** nell'istanza di SQL Server primaria

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2 Aggiungere l'account di accesso all'istanza di SQL Server secondaria

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 Aggiornare la stringa di connessione usata per la registrazione.
Chiamare la stored procedure `[catalog].[update_logdb_info]` usando i valori di parametro seguenti:

-   `@server_name = '[Availability Group Listener DNS name],[Port]' `

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-failover-cluster"></a>7. Configurare il ruolo del servizio Scale Out Master del cluster di failover di Windows

1.  In Gestione cluster di failover connettersi al cluster per Scale Out. Selezionare il cluster. Selezionare **Azione** dal menu e poi **Configura ruolo**.

2.  Nella finestra di dialogo **Configurazione guidata disponibilità elevata** selezionare **Servizio generico** nella pagina **Selezione ruolo**. Selezionare SQL Server Integration Services Scale Out Master 14.0 nella pagina **Seleziona servizio**.

3.  Nella pagina **Punto di accesso client** immettere il nome host DNS del servizio Scale Out Master.

    ![Configurazione guidata disponibilità elevata 1](media/ha-wizard1.PNG)

4.  Completare la procedura guidata.

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8. Aggiornare l'indirizzo di Scale Out Master nel database SSISDB

Nell'istanza di SQL Server primaria eseguire la stored procedure `[catalog].[update_master_address]` con il valore di parametro `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'`. 

## <a name="9-add-the-scale-out-workers"></a>9. Aggiungere le istanze di Scale Out Worker

A questo punto è possibile aggiungere le istanze di Scale Out Worker usando [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md). Immettere `[SQL Server Availability Group Listener DNS name],[Port]` nella pagina di connessione.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere gli articoli seguenti:
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)