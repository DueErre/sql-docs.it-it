---
title: "Proprietà pubblicazione, Snapshot | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38e2f81f0b5f1c0de7a07989e9b768e595c0670b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="publication-properties-snapshot"></a>Proprietà pubblicazione, Snapshot
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione** consente di impostare il formato dello snapshot, il percorso dello snapshot e gli script da eseguire prima e dopo l'applicazione dello snapshot. La cartella dello snapshot deve essere designata come condivisione e disporre delle autorizzazioni sufficienti per la lettura e la scrittura dei file nella cartella da parte degli agenti. Per altre informazioni sulle impostazioni di sicurezza appropriate per la cartella, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
> [!NOTE]  
>  In caso di modifiche, sarà necessario un nuovo snapshot per la pubblicazione. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## <a name="options"></a>Opzioni  
 **Formato snapshot**  
 Consente di selezionare la modalità nativa o la modalità carattere per il formato dello snapshot.  
  
-   Selezionare **Formato nativo di SQL Server: tutti i Sottoscrittori devono essere server che eseguono SQL Server** se tutti i Sottoscrittori sono istanze di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diverse da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Il formato nativo dello snapshot offre le migliori prestazioni.  
  
-   Selezionare **Carattere: obbligatorio se in un server di pubblicazione o in un Sottoscrittore non è in esecuzione SQL Server** se uno o più Sottoscrittori eseguono [!INCLUDE[ssEW](../../includes/ssew-md.md)] oppure non sono Sottoscrittori[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Percorso dei file di snapshot**  
 Consente di selezionare il percorso per l'archiviazione dei file di snapshot. Questi file possono essere archiviati nel percorso predefinito. È inoltre possibile archiviarli in un percorso alternativo in sostituzione o in aggiunta al percorso predefinito. I file archiviati in un percorso alternativo possono essere archiviati.  
  
-   Selezionare **Inserisci i file nella cartella predefinita** per utilizzare la cartella dello snapshot predefinita per il server di pubblicazione. Il percorso dello snapshot in questa finestra di dialogo è di sola lettura, poiché può essere modificato per il server di pubblicazione solo nella finestra di dialogo **Proprietà server di distribuzione** . Per altre informazioni, vedere [Specificare la posizione predefinita degli snapshot &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   Selezionare **Inserisci i file nella cartella seguente** per specificare un percorso alternativo in sostituzione o in aggiunta al percorso predefinito. Immettere un percorso nella casella di testo oppure fare clic su **Sfoglia** per selezionare un percorso. Selezionare **Comprimi i file di snapshot in questa cartella** per comprimere i file nel percorso dello snapshot alternativo. Il percorso alternativo può trovarsi in un altro server, in un'unità di rete oppure in un supporto rimovibile, ad esempio un CD-ROM o un disco rimovibile. Per ulteriori informazioni, vedere [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md) e [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md).  
  
 **Script aggiuntivi**  
 Consente di specificare gli script da eseguire prima e dopo l'applicazione dello snapshot nel Sottoscrittore. Non è possibile specificare gli script se l'opzione **Formato snapshot** è impostata su **Carattere**.  
  
 L'utilizzo degli script è facoltativo, tuttavia esso rappresenta un metodo pratico per eseguire comandi e applicare modifiche amministrative nei Sottoscrittori. Per altre informazioni sull'esecuzione di script, vedere [Eseguire gli script prima e dopo l'applicazione dello snapshot](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Immettere un percorso nella casella di testo **Prima di applicare lo snapshot, esegui lo script seguente** oppure fare clic su **Sfoglia** per selezionare il percorso dello script.  
  
-   Immettere un percorso nella casella di testo **Dopo l'applicazione dello snapshot, esegui lo script seguente** oppure fare clic su **Sfoglia** per selezionare il percorso dello script.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Creare e applicare lo snapshot iniziale](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
