---
title: Oggetto procedure (ADOX) | Documenti Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Procedure
helpviewer_keywords:
- Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 225a864f43c9da7d67de58482f632b914822bd1b
ms.contentlocale: it-it
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-object-adox"></a>Oggetto procedure (ADOX)
Rappresenta una stored procedure. Quando utilizzato in combinazione con l'oggetto ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto, il **procedura** oggetto può essere utilizzato per l'aggiunta, eliminazione o modifica di stored procedure.  
  
## <a name="remarks"></a>Osservazioni  
 Il **procedura** oggetto consente di creare una stored procedure senza la necessità di conoscere o utilizzare sintassi di "CREATE PROCEDURE" del provider.  
  
 Con le proprietà di un **procedura** dell'oggetto, è possibile:  
  
-   Identificare la procedura con il [nome](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Specificare l'oggetto ADO **comando** oggetto che può essere usato per creare o eseguire la procedura con il [comando](../../../ado/reference/adox-api/command-property-adox.md) proprietà.  
  
-   Restituire informazioni relative alla data con la [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) proprietà.  
  
 In questa sezione contiene l'argomento seguente.  
  
-   [Le proprietà dell'oggetto stored procedure, metodi ed eventi](../../../ado/reference/adox-api/procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Comando e l'esempio di proprietà CommandText (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Raccolta di parametri, esempio di proprietà di comando (Visual Basic)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Procedure di esempio del metodo Append (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Procedure di esempio del metodo Delete (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Raccolta di procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)