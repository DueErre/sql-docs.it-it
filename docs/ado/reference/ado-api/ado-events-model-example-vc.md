---
title: Esempio (VC + +) del modello di eventi ADO | Documenti Microsoft
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
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ code examples [ADO], event model
ms.assetid: 29530153-b963-4a7c-8665-2335f1d604a8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e141eadd6f641608ccef1fb6b1b48b4138bf2728
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="ado-events-model-example-vc"></a>Esempio di modello di eventi ADO (VC + +)
La sezione di Visual C++ di [la creazione di istanze di ADO evento dal linguaggio](../../../ado/guide/data/ado-event-instantiation-by-language.md) viene fornita una descrizione generale di creazione di un'istanza del modello di evento ADO. Ecco un esempio specifico di un'istanza del modello di evento all'interno dell'ambiente creato tramite il **#import** direttiva.  
  
 Descrizione generale utilizza **adoint** come riferimento per le firme del metodo. Tuttavia, alcuni dettagli della descrizione generale variano leggermente in seguito all'utilizzo di **#import** direttiva:  
  
-   Il **#import** direttiva risolve **typedef**del, tipi di dati della firma di metodo, ai modificatori e ai moduli fondamentali.  
  
-   I metodi virtuali puri che devono essere sovrascritti sono preceduti da "**raw _**".  
  
 Parte del codice semplicemente riflette dello stile di codifica.  
  
-   Puntatore a **IUnknown** utilizzato il **Advise** metodo ottenuto in modo esplicito con una chiamata a **QueryInterface**.  
  
-   Non è necessario codificare in modo esplicito un distruttore nelle definizioni di classe.  
  
-   Si consiglia di codice più affidabile implementazioni di QueryInterface, AddRef e Release.  
  
-   Il **__uuidof()** direttiva è ampiamente utilizzata per ottenere gli ID di interfaccia.  
  
 Infine, l'esempio contiene codice funzionante.  
  
-   Nell'esempio viene scritta come un'applicazione console.  
  
-   È necessario inserire il proprio codice sotto il commento "`// Do some work`".  
  
-   Tutte le evento gestori predefiniti eseguire alcuna operazione e annullano eventuali notifiche. Inserire il codice appropriato per l'applicazione e consente le notifiche, se necessario.  
  
```  
// ADO_Events_Model_Example.cpp  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// The Connection events  
class CConnEvent : public ConnectionEventsVt {  
private:  
   ULONG m_cRef;  
  
public:  
   CConnEvent() { m_cRef = 0; };  
   ~CConnEvent() {};  
  
   STDMETHODIMP QueryInterface(REFIID riid, void ** ppv);  
   STDMETHODIMP_(ULONG) AddRef();  
   STDMETHODIMP_(ULONG) Release();  
  
   STDMETHODIMP raw_InfoMessage( struct Error *pError,   
                                 EventStatusEnum *adStatus,   
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_BeginTransComplete( LONG TransactionLevel,  
                                        struct Error *pError,  
                                        EventStatusEnum *adStatus,  
                                        struct _Connection *pConnection);  
  
   STDMETHODIMP raw_CommitTransComplete( struct Error *pError,   
                                         EventStatusEnum *adStatus,  
                                         struct _Connection *pConnection);  
  
   STDMETHODIMP raw_RollbackTransComplete( struct Error *pError,   
                                           EventStatusEnum *adStatus,  
                                           struct _Connection *pConnection);  
  
   STDMETHODIMP raw_WillExecute( BSTR *Source,  
                                 CursorTypeEnum *CursorType,  
                                 LockTypeEnum *LockType,  
                                 long *Options,  
                                 EventStatusEnum *adStatus,  
                                 struct _Command *pCommand,  
                                 struct _Recordset *pRecordset,  
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_ExecuteComplete( LONG RecordsAffected,  
                                     struct Error *pError,  
                                     EventStatusEnum *adStatus,  
                                     struct _Command *pCommand,  
                                     struct _Recordset *pRecordset,  
                                     struct _Connection *pConnection);  
  
   STDMETHODIMP raw_WillConnect( BSTR *ConnectionString,  
                                 BSTR *UserID,  
                                 BSTR *Password,  
                                 long *Options,  
                                 EventStatusEnum *adStatus,  
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_ConnectComplete( struct Error *pError,  
                                     EventStatusEnum *adStatus,  
                                     struct _Connection *pConnection);  
  
   STDMETHODIMP raw_Disconnect( EventStatusEnum *adStatus, struct _Connection *pConnection);  
};  
  
// The Recordset events  
class CRstEvent : public RecordsetEventsVt {  
private:  
   ULONG m_cRef;     
  
public:  
   CRstEvent() { m_cRef = 0; };  
   ~CRstEvent() {};  
  
   STDMETHODIMP QueryInterface(REFIID riid, void ** ppv);  
   STDMETHODIMP_(ULONG) AddRef();  
   STDMETHODIMP_(ULONG) Release();  
  
   STDMETHODIMP raw_WillChangeField( LONG cFields,        
                                     VARIANT Fields,  
                                     EventStatusEnum *adStatus,  
                                     struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FieldChangeComplete( LONG cFields,  
                                         VARIANT Fields,  
                                         struct Error *pError,  
                                         EventStatusEnum *adStatus,  
                                         struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillChangeRecord( EventReasonEnum adReason,  
                                      LONG cRecords,  
                                      EventStatusEnum *adStatus,  
                                      struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_RecordChangeComplete( EventReasonEnum adReason,  
                                          LONG cRecords,  
                                          struct Error *pError,  
                                          EventStatusEnum *adStatus,  
                                          struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillChangeRecordset( EventReasonEnum adReason,  
                                         EventStatusEnum *adStatus,  
                                         struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_RecordsetChangeComplete( EventReasonEnum adReason,  
                                             struct Error *pError,  
                                             EventStatusEnum *adStatus,  
                                             struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillMove( EventReasonEnum adReason,  
                              EventStatusEnum *adStatus,  
                              struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_MoveComplete( EventReasonEnum adReason,  
                                  struct Error *pError,  
                                  EventStatusEnum *adStatus,  
                                  struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_EndOfRecordset( VARIANT_BOOL *fMoreData,  
                                    EventStatusEnum *adStatus,  
                                    struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FetchProgress( long Progress,  
                                   long MaxProgress,  
                                   EventStatusEnum *adStatus,  
                                   struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FetchComplete( struct Error *pError,   
                                   EventStatusEnum *adStatus,  
                                   struct _Recordset *pRecordset);  
};  
  
// Implement each connection method  
STDMETHODIMP CConnEvent::raw_InfoMessage( struct Error *pError,   
                                         EventStatusEnum *adStatus,  
                                         struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_BeginTransComplete( LONG TransactionLevel,  
                                                 struct Error *pError,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_CommitTransComplete( struct Error *pError,  
                                                  EventStatusEnum *adStatus,  
                                                  struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_RollbackTransComplete( struct Error *pError,  
                                                    EventStatusEnum *adStatus,  
                                                    struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_WillExecute( BSTR *Source,  
                                          CursorTypeEnum *CursorType,  
                                          LockTypeEnum *LockType,  
                                          long *Options,  
                                          EventStatusEnum *adStatus,  
                                          struct _Command *pCommand,  
                                          struct _Recordset *pRecordset,  
                                          struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_ExecuteComplete( LONG RecordsAffected,  
                                              struct Error *pError,  
                                              EventStatusEnum *adStatus,  
                                              struct _Command *pCommand,  
                                              struct _Recordset *pRecordset,  
                                              struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_WillConnect( BSTR *ConnectionString,  
                                          BSTR *UserID,  
                                          BSTR *Password,  
                                          long *Options,  
                                          EventStatusEnum *adStatus,  
                                          struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_ConnectComplete( struct Error *pError,  
                                              EventStatusEnum *adStatus,  
                                              struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_Disconnect( EventStatusEnum *adStatus, struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
// Implement each recordset method  
STDMETHODIMP CRstEvent::raw_WillChangeField( LONG cFields,  
                                             VARIANT Fields,  
                                             EventStatusEnum *adStatus,  
                                             struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FieldChangeComplete( LONG cFields,  
                                                 VARIANT Fields,  
                                                 struct Error *pError,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillChangeRecord( EventReasonEnum adReason,  
                                              LONG cRecords,  
                                              EventStatusEnum *adStatus,  
                                              struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_RecordChangeComplete( EventReasonEnum adReason,  
                                                  LONG cRecords,  
                                                  struct Error *pError,  
                                                  EventStatusEnum *adStatus,  
                                                  struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillChangeRecordset( EventReasonEnum adReason,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_RecordsetChangeComplete( EventReasonEnum adReason,  
                                                     struct Error *pError,  
                                                     EventStatusEnum *adStatus,  
                                                     struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillMove( EventReasonEnum adReason,   
                                      EventStatusEnum *adStatus,  
                                      struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_MoveComplete( EventReasonEnum adReason,  
                                          struct Error *pError,  
                                          EventStatusEnum *adStatus,  
                                          struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_EndOfRecordset( VARIANT_BOOL *fMoreData,  
                                            EventStatusEnum *adStatus,  
                                            struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FetchProgress( long Progress,  
                                           long MaxProgress,  
                                           EventStatusEnum *adStatus,  
                                           struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FetchComplete( struct Error *pError,  
                                           EventStatusEnum *adStatus,  
                                           struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::QueryInterface(REFIID riid, void ** ppv) {  
   *ppv = NULL;  
   if (riid == __uuidof(IUnknown) || riid == __uuidof(RecordsetEventsVt))   
      *ppv = this;  
  
   if (*ppv == NULL)  
      return ResultFromScode(E_NOINTERFACE);  
  
   AddRef();  
   return NOERROR;  
}  
  
STDMETHODIMP_(ULONG) CRstEvent::AddRef() {   
   return ++m_cRef;   
};  
  
STDMETHODIMP_(ULONG) CRstEvent::Release() {   
   if (0 != --m_cRef)   
      return m_cRef;  
   delete this;  
   return 0;  
}  
  
STDMETHODIMP CConnEvent::QueryInterface(REFIID riid, void ** ppv) {  
   *ppv = NULL;  
   if (riid == __uuidof(IUnknown) || riid == __uuidof(ConnectionEventsVt))   
      *ppv = this;  
  
   if (*ppv == NULL)  
      return ResultFromScode(E_NOINTERFACE);  
  
   AddRef();  
   return NOERROR;  
}  
  
STDMETHODIMP_(ULONG) CConnEvent::AddRef() {   
   return ++m_cRef;   
};  
  
STDMETHODIMP_(ULONG) CConnEvent::Release() {   
   if (0 != --m_cRef)   
      return m_cRef;  
   delete this;  
   return 0;  
}  
  
int main() {  
   HRESULT hr;  
   DWORD dwConnEvt;  
   DWORD dwRstEvt;  
   IConnectionPointContainer *pCPC = NULL;  
   IConnectionPoint *pCP = NULL;  
   IUnknown *pUnk = NULL;  
   CRstEvent *pRstEvent = NULL;  
   CConnEvent *pConnEvent= NULL;  
   int rc = 0;  
   _RecordsetPtr pRst;   
   _ConnectionPtr pConn;  
  
   ::CoInitialize(NULL);  
  
   hr = pConn.CreateInstance(__uuidof(Connection));  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pRst.CreateInstance(__uuidof(Recordset));  
  
   if (FAILED(hr))   
      return rc;  
  
   // Start using the Connection events  
   hr = pConn->QueryInterface(__uuidof(IConnectionPointContainer), (void **)&pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(ConnectionEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   pConnEvent = new CConnEvent();  
   hr = pConnEvent->QueryInterface(__uuidof(IUnknown), (void **) &pUnk);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Advise(pUnk, &dwConnEvt);  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Start using the Recordset events  
   hr = pRst->QueryInterface(__uuidof(IConnectionPointContainer), (void **)&pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(RecordsetEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   pRstEvent = new CRstEvent();  
   hr = pRstEvent->QueryInterface(__uuidof(IUnknown), (void **) &pUnk);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Advise(pUnk, &dwRstEvt);  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Do some work  
   pConn->Open("dsn=DataPubs;", "", "", adConnectUnspecified);  
   pRst->Open("SELECT * FROM authors", (IDispatch *) pConn, adOpenStatic, adLockReadOnly, adCmdText);  
  
   pRst->MoveFirst();  
   while (pRst->EndOfFile == FALSE) {  
      wprintf(L"Name = '%s'\n", (wchar_t*) ((_bstr_t) pRst->Fields->GetItem("au_lname")->Value));  
      pRst->MoveNext();  
   }  
  
   pRst->Close();  
   pConn->Close();  
  
   // Stop using the Connection events  
   hr = pConn->QueryInterface(__uuidof(IConnectionPointContainer), (void **) &pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(ConnectionEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Unadvise( dwConnEvt );  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Stop using the Recordset events  
   hr = pRst->QueryInterface(__uuidof(IConnectionPointContainer), (void **) &pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(RecordsetEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Unadvise( dwRstEvt );  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   CoUninitialize();  
}  
```
