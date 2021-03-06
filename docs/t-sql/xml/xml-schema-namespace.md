---
title: xml_schema_namespace (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19f4701bc26e115c7f6b78d01feef876665763df
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ricostruisce tutti gli schemi o uno schema specifico nella raccolta di XML Schema specificata. Questa funzione restituisce un'istanza del tipo di dati **xml** .  
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Relational_schema*  
 Nome dello schema relazionale. *Relational_schema* è **sysname**.  
  
 *XML_schema_collection_name*  
 Nome della raccolta di XML Schema da ricostruire. *XML_schema_collection_name* è **sysname**.  
  
 *Spazio dei nomi*  
 Spazio dei nomi URI di XML Schema che si desidera ricostruire. La lunghezza massima è 1000 caratteri. Se l'URI dello spazio dei nomi viene omesso, viene ricostruita l'intera raccolta di XML Schema. *Namespace* è **nvarchar (4000)**.  
  
## <a name="return-types"></a>Tipi restituiti  
 **xml**  
  
## <a name="remarks"></a>Osservazioni  
 Quando si importano i componenti di schema XML nel database utilizzando [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) o [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md), vengono mantenuti gli aspetti dello schema utilizzato per la convalida. Pertanto, lo schema ricostruito può non corrispondere al documento dello schema originale dal punto di vista lessicale. Più specificamente, vengono persi i commenti, gli spazi vuoti e le annotazioni, mentre le informazioni implicite sui tipi vengono rese esplicite. Ad esempio, \<xs: element name = "e1" / > diventa \<xs: element name = "e1" type = "xs: anyType" / >. Inoltre, non vengono mantenuti i prefissi degli spazi dei nomi.  
  
 Se si specifica un parametro relativo allo spazio dei nomi, il documento dello schema risultante conterrà le definizioni per tutti i componenti degli schemi in quello spazio dei nomi, anche se erano state aggiunte in passaggi DDL o documenti di schemi diversi, o in entrambi.  
  
 È possibile utilizzare questa funzione per costruire documenti di XML schema dal **sys.sys** raccolta di XML schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene recuperata la raccolta di XML Schema `ProductDescriptionSchemaCollection` dallo schema relazionale di produzione nel database `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare una raccolta di XML Schema archiviata](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Raccolte di XML Schema &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
