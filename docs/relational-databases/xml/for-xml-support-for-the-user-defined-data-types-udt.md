---
title: Supporto di FOR XML per i tipi di dati definiti dall'utente (UDT) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf91171be35a102b77a563478e4c036276fff855
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Supporto di FOR XML per i tipi di dati definiti dall'utente (UDT)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] FOR XML non supporta tipi di dati definiti dall'utente Common Language Runtime (CLR).  
  
 Per utilizzare FOR XML con tipi di dati definiti dall'utente CLR, assicurarsi che il tipo di dati abbia una serializzazione XML e utilizzare un cast esplicito per XML nella clausola scelta FOR XML.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di FOR XML per vari tipi di dati di SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
