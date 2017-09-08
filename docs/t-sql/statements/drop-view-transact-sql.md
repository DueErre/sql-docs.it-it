---
title: DROP VIEW (Transact-SQL) | Documenti Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8dedeff21f56659d0cc55eef2d133a1ecbe0f63e
ms.contentlocale: it-it
ms.lasthandoff: 09/01/2017

---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Rimuove una o più viste dal database corrente. È possibile eseguire l'istruzione DROP VIEW su viste indicizzate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *SE ESISTE*  
 **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] tramite [versione corrente](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]). |  
  
 Elimina in modo condizionale la visualizzazione solo se esiste già.  
  
 *schema_name*  
 Nome dello schema a cui appartiene la vista.  
  
 *view_name*  
 Nome della vista da rimuovere.  
  
## <a name="remarks"></a>Osservazioni  
 Quando si rimuove una vista, dal catalogo di sistema vengono eliminate la definizione e altre informazioni della vista. Vengono inoltre eliminate tutte le autorizzazioni per la vista.  
  
 Qualsiasi vista di una tabella che viene eliminata tramite DROP TABLE deve essere eliminata in modo esplicito con DROP VIEW.  
  
 Quando viene eseguita su una vista indicizzata, l'istruzione DROP VIEW elimina automaticamente tutti gli indici della vista. Per visualizzare tutti gli indici in una vista, utilizzare [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 Quando si esegue una query tramite una vista, [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica che tutti gli oggetti di database a cui viene fatto riferimento nell'istruzione esistano e siano validi nel contesto dell'istruzione. Inoltre, verifica che le istruzioni di modifica dei dati non violino le regole di integrità dei dati. Se la verifica ha esito negativo, viene visualizzato un messaggio di errore. In caso contrario, l'azione viene convertita automaticamente in un'operazione sulla tabella o sulle tabelle sottostanti. Se le tabelle o viste sottostanti sono state modificate dopo la creazione della vista, può risultare utile eliminare e ricreare la vista.  
  
 Per ulteriori informazioni sulla determinazione delle dipendenze per una vista specifica, vedere [sql_dependencies &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 Per ulteriori informazioni sulla visualizzazione del testo della visualizzazione, vedere [sp_helptext &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Richiede **controllo** l'autorizzazione per la visualizzazione, **ALTER** autorizzazione per lo schema contenente la vista o l'appartenenza di **db_ddladmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-drop-a-view"></a>A. Eliminare una vista  
 Nell'esempio seguente si rimuove la vista `Reorder`.  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Usa &#40; Transact-SQL &#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 
