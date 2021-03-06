---
title: ErrorValueEnum | Documenti Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a79af3564a177da2953b053ce943a2d740e4cc7d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="errorvalueenum"></a>ErrorValueEnum
Specifica il tipo di errore di run-time di ADO.  
  
 Sono elencati tre forme del numero di errore:  
  
-   Decimale positivo, i due byte inferiori del numero completo in formato decimale. Questo numero viene visualizzato nella finestra di dialogo predefinita Visual Basic errore messaggio. Ad esempio, errore di Run-time '3707'.  
  
-   Decimale negativo, la conversione decimale del numero di errore completo.  
  
-   Esadecimale, ovvero la rappresentazione esadecimale del numero di errore completo. Il codice di funzionalità di Windows è la quarta cifra. Il codice della funzionalità per i numeri di errore ADO *A*. Ad esempio: 0x800***A***0E7B.  
  
> [!NOTE]
>  Errori OLE DB possono essere passati all'applicazione ADO. In genere, possono essere identificati da un codice di funzionalità di Windows di *4*. Ad esempio, 0x800***4***.  
  
|Costante|Valore|Description|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707 -2146824581 0x800A0E7B|Non è possibile modificare il **ActiveConnection** proprietà di un **Recordset** oggetto che ha un **comando** oggetto come origine.|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|Impossibile completare l'operazione.|  
|**adErrCantChangeConnection**|3748 -2146824540 0x800A0EA4|Connessione è stata negata. Nuova connessione richiesta ha caratteristiche diverse rispetto a quella già in uso.|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|Il provider specificato è diverso da quello già in uso.|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|Impossibile convertire il valore di dati per motivi diversi overflow di dati o non corrispondenza del segno. Ad esempio, conversione causi il troncamento dei dati.|  
|**adErrCantCreate**|3725 -2146824563 0x800A0E8D|Valore di dati non può essere impostato o recuperato perché il tipo di dati del campo è sconosciuto, o il provider ha risorse insufficienti per eseguire l'operazione.|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|Operazione richiede un valore valido **ParentCatalog**.|  
|**adErrColumnNotOnThisRow**|3726 -2146824562 0x800A0E8E|Record non contiene questo campo.|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|Applicazione utilizza un valore di tipo errato per l'operazione corrente.|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|Il valore di dati è troppo grande per essere rappresentato dal tipo di dati di campo.|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|URL dell'oggetto da eliminare è all'esterno dell'ambito del record corrente.|  
|**adErrDenyNotSupported**|3750 -2146824538 0x800A0EA6|Provider non supporta le restrizioni di condivisione.|  
|**adErrDenyTypeNotSupported**|3751 -2146824537 0x800A0EA7|Provider non supporta il tipo richiesto restrizione della condivisione.|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|Oggetto o il provider non è in grado di eseguire l'operazione richiesta.|  
|**adErrFieldsUpdateFailed**|3749 -2146824539 0x800A0EA5|Impossibile aggiornare i campi. Per ulteriori informazioni, esaminare il **stato** proprietà degli oggetti singoli campi.|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|Operazione non è consentita in questo contesto.|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|Il valore dei dati è in conflitto con i vincoli di integrità del campo.|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**Connessione** oggetto non può essere chiusa in modo esplicito in una transazione.|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|Gli argomenti sono di tipo errato, sono compreso nell'intervallo accettabile o sono in conflitto.|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|La connessione non può essere utilizzata per eseguire questa operazione. È chiuso o non valido in questo contesto.|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**Parametro** oggetto è definito in modo errato. Informazioni incomplete o è state specificate.|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|Il coordinamento della transazione non è valido o non è stato avviato.|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|L'URL contiene caratteri non validi. Assicurarsi che l'URL sia stato digitato correttamente.|  
|**adErrItemNotFound**|3265 -2146825023 0x800A0CC1|Impossibile trovare l'elemento della raccolta che corrisponde al nome richiesto o per ordinale.|  
|**adErrNoCurrentRecord**|3021 -2146825267 0x800A0BCD|Entrambi **BOF** o **EOF** è True, o il record corrente è stato eliminato. Operazione richiesta richiede un record corrente.|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|Operazione non può essere eseguita anche se non in esecuzione.|  
|**adErrNotReentrant**|3710 -2146824578 0x800A0E7E|Impossibile eseguire l'operazione durante l'elaborazione dell'evento.|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|Operazione non è consentita quando l'oggetto viene chiuso.|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|Oggetto è già nella raccolta. Impossibile accodare.|  
|**adErrObjectNotSet**|3420 -2146824868 0x800A0D5C|Oggetto non è più valido.|  
|**adErrObjectOpen**|3705 -2146824583 0x800A0E79|Operazione non è consentita quando l'oggetto è aperto.|  
|**adErrOpeningFile**|3002 -2146825286 0x800A0BBA|Impossibile aprire il file.|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|Operazione annullata dall'utente.|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|Impossibile eseguire l'operazione. Il provider non è possibile ottenere spazio di archiviazione sufficiente.|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|Autorizzazioni insufficienti impediscono la scrittura del campo.|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|Provider non eseguire l'operazione richiesta.|  
|**adErrProviderNotFound**|3706 -2146824582 0x800A0E7A|Impossibile trovare il provider. Si potrebbe non essere installato correttamente.|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|Non è stato possibile leggere i file.|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|Impossibile eseguire l'operazione di copia. Oggetto denominato dall'URL di destinazione già esistente. Specificare **adCopyOverwrite** di sostituire l'oggetto.|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|Oggetto rappresentato dall'URL specificato è bloccato da uno o più processi. Attendere il termine del processo e ripetere l'operazione.|  
|**adErrResourceOutOfScope**|3735 -2146824553 0x800A0E97|URL di origine o di destinazione è all'esterno dell'ambito del record corrente.|  
|**adErrSchemaViolation**|3722 -2146824566 0x800A0E8A|Il valore dei dati è in conflitto con il tipo di dati o i vincoli del campo.|  
|**adErrSignMismatch**|3723 -2146824565 0x800A0E8B|Conversione non riuscita perché il valore dei dati è con segno mentre il tipo di dati di campo utilizzato dal provider è senza segno.|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|Impossibile eseguire l'operazione durante la connessione in modo asincrono.|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|Impossibile eseguire l'operazione durante l'esecuzione in modo asincrono.|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|Autorizzazioni non sono sufficienti per accedere a struttura ad albero o sottoalbero.|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|Operazione non completata e lo stato non è disponibile. Il campo può essere non disponibile o non è stata tentata l'operazione.|  
|**adErrUnsafeOperation**|3716 -2146824572 0x800A0E84|Le impostazioni di protezione nel computer impediscono l'accesso a un'origine dati in un altro dominio.|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|L'URL di origine o l'elemento padre dell'URL di destinazione non esiste.|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|Il record specificato da questo URL non esiste.|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|Impossibile individuare il dispositivo di archiviazione indicato dall'URL. Assicurarsi che l'URL sia stato digitato correttamente.|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|Impossibile scrivere nel file.|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|Solo per uso interno. Non usare.|  
|**adWrnSecurityDialogHeader**|3718 -2146824570 0x800A0E86|Solo per uso interno. Non usare.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Package: **com.ms.wfc.data**  
  
 Solo il subset seguente di equivalenti in ADO/WFC sono definiti.  
  
|Costante|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Codici di errore ADO](../../../ado/guide/appendixes/ado-error-codes.md)
