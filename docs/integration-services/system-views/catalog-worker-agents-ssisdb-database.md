---
title: catalog.worker_agents (database SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b3d7ae2666a6adc774093a8496863685457e7e6
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents (database SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Visualizza le informazioni su [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker.

|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|ID agente di lavoro dello Scale Out Worker.|
|IsEnabled|**bit**|Indica se Scale Out Worker è abilitato.|
|DisplayName|**nvarchar(256)**|Nome visualizzato di Scale Out Worker.|
|Description|**nvarchar(256)**|Descrizione di Scale Out Worker.|
|MachineName|**nvarchar(256)**|Nome computer di Scale Out Worker.|
|Tag|**nvarchar(max)**|Tag di Scale Out Worker.|
|UserAccount|**nvarchar(256)**|Account che esegue il servizio Scale Out Worker.|
|LastOnlineTime|**datetimeoffset(7)**|Ultima esecuzione online del servizio Scale Out Worker.|

## <a name="remarks"></a>Remarks
Questa vista mostra una riga per ogni Scale Out Worker che si connette allo Scale Out Master che interagisce con il catalogo SSISDB.

## <a name="permissions"></a>Autorizzazioni
Per questa vista è necessaria una delle autorizzazioni seguenti:

- Appartenenza al ruolo del database **ssis_admin**

- Appartenenza al ruolo del database **ssis_cluster_executor**

- Appartenenza al ruolo del server **sysadmin**
