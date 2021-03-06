---
title: Definire e modificare un filtro di riga con parametri per un articolo di merge | Microsoft Docs
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
helpviewer_keywords:
- parameterized filters [SQL Server replication], defining
- parameterized filters [SQL Server replication], modifying
- merge replication [SQL Server replication], dynamic filters
- merge replication parameterized filters [SQL Server replication]
- filters [SQL Server replication], parameterized
- modifying filters, parameterized row
- dynamic filters [SQL Server replication]
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: "44"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a199039c0535cb3eb7fee8accadcdb28ecf12ed2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="define-and-modify-a-parameterized-row-filter-for-a-merge-article"></a>Definizione e modifica di un filtro di riga con parametri per un articolo di merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Questo argomento descrive come definire e modificare un filtro di riga con parametri in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Quando si creano articoli di tabella, è possibile usare filtri di riga con parametri. Questi filtri usano una clausola [WHERE](../../../t-sql/queries/where-transact-sql.md) per selezionare i dati adatti da pubblicare. Anziché specificare un valore letterale nella clausola, come avviene con il filtro di riga statico, si specificano una o entrambe le funzioni di sistema seguenti: [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) e [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md). Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
-   **Per definire e modificare un filtro di riga con parametri, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se si aggiunge, modifica o elimina un filtro di riga con parametri dopo che sono state inizializzate sottoscrizioni per la pubblicazione, è necessario generare un nuovo snapshot e reinizializzare tutte le sottoscrizioni in seguito alla modifica. Per altre informazioni sui requisiti per la modifica delle proprietà, vedere [Modificare le proprietà di pubblicazioni e articoli](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Per motivi relativi alle prestazioni è consigliabile evitare di applicare funzioni ai nomi di colonna nelle clausole per filtri di riga con parametri, come `LEFT([MyColumn]) = SUSER_SNAME()`. Se si usano HOST_NAME in una clausola di filtro e si sostituisce il valore HOST_NAME, può essere necessario convertire i tipi di dati tramite l'istruzione CONVERT. Per altre informazioni sulle procedure consigliate in questo caso, vedere la sezione relativa alla sostituzione del valore HOST_NAME() nell'argomento [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Definire, modificare ed eliminare filtri di riga con parametri nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione oppure nella pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](../../../relational-databases/replication/publish/create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-parameterized-row-filter"></a>Per definire un filtro di riga con parametri  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione oppure nella pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **Aggiungi** e quindi su **Aggiungi filtro**.  
  
2.  Nella finestra di dialogo **Aggiungi filtro** selezionare una tabella da filtrare nell'elenco a discesa.  
  
3.  Creare un'istruzione di filtro nella casella di testo **Istruzione per il filtro** . È possibile digitare direttamente nell'area di testo nonché trascinare colonne dalla casella di riepilogo **Colonne** .  
  
    -   L'area di testo **Istruzione per il filtro** contiene il testo predefinito, nel formato seguente:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   Il testo predefinito non può essere modificato. Digitare la clausola di filtro dopo la parola chiave WHERE usando la sintassi SQL standard. Un filtro con parametri include una chiamata alla funzione di sistema **HOST_NAME()** e/o **SUSER_SNAME()**oppure a una funzione definita dall'utente che fa riferimento a una di queste funzioni o a entrambe. Di seguito è riportato un esempio di una clausola di filtro completa per un filtro di riga con parametri:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         Per la clausola WHERE è consigliabile usare nomi in due parti. I nomi in tre e quattro parti non sono supportati.  
  
4.  Selezionare l'opzione corrispondente alla modalità desiderata di condivisione dei dati tra i Sottoscrittori:  
  
    -   **Una riga di questa tabella verrà inviata a più sottoscrizioni**  
  
    -   **Una riga di questa tabella verrà inviata a una sola sottoscrizione**  
  
     Selezionando **Una riga di questa tabella verrà inviata a una sola sottoscrizione**è possibile ottimizzare le prestazioni della replica di tipo merge archiviando ed elaborando una minore quantità di metadati. È tuttavia necessario garantire che i dati vengano partizionati in modo da non consentire la replica di una riga in più Sottoscrittori. Per altre informazioni, vedere la sezione relativa all'impostazione delle opzioni delle partizioni nell'argomento [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Se è visualizzata la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** fare clic su **OK** per salvare e chiudere la finestra di dialogo.  
  
#### <a name="to-modify-a-parameterized-row-filter"></a>Per modificare un filtro di riga con parametri  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtro righe** di **Proprietà pubblicazione - \<Pubblicazione>** selezionare un filtro nel riquadro **Tabelle filtrate** e quindi fare clic su **Modifica**.  
  
2.  Nella finestra di dialogo **Modifica filtro** modificare il filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-parameterized-row-filter"></a>Per eliminare un filtro di riga con parametri  
  
1.  Nella pagina **Filtro righe tabella** della Creazione guidata nuova pubblicazione o nella pagina **Filtro righe** di **Proprietà pubblicazione - \<Pubblicazione>** selezionare un filtro nel riquadro **Tabelle filtrate** e quindi fare clic su **Elimina**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 È possibile creare e modificare a livello di programmazione i filtri di riga con parametri tramite le stored procedure di replica.  
  
#### <a name="to-define-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>Per definire un filtro di riga con parametri per un articolo in una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Specificare **@publication**, un nome di articolo per **@article**, la tabella da pubblicare per **@source_object**, la clausola WHERE che definisce il filtro con parametri per **@subset_filterclause** (escluso `WHERE`) e uno dei valori seguenti per **@partition_options**, che descrive il tipo di partizionamento risultante dall'applicazione del filtro di riga con parametri:  
  
    -   **0** : il filtro dell'articolo è statico oppure non restituisce un subset univoco di dati per ogni partizione, ovvero si tratta di una partizione "sovrapposta".  
  
    -   **1** : le partizioni risultanti sono sovrapposte e gli aggiornamenti apportati nel Sottoscrittore non possono modificare la partizione a cui appartiene una riga.  
  
    -   **2** : il filtro dell'articolo restituisce partizioni non sovrapposte, ma più Sottoscrittori ricevono la stessa partizione.  
  
    -   **3** : il filtro dell'articolo restituisce partizioni non sovrapposte univoche per ogni sottoscrizione.  
  
#### <a name="to-change-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>Per modificare un filtro di riga con parametri per un articolo in una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Specificare **@publication**, **@article**, il valore **subset_filterclause** per **@property**, l'espressione che definisce il filtro con parametri per **@value** (escluso `WHERE`) e il valore **1** sia per **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Se questa modifica implica un diverso comportamento del partizionamento, eseguire nuovamente [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) . Specificare **@publication**, **@article**, il valore **partition_options** per **@property**e l'opzione di partizionamento più appropriata tra quelle elencate di seguito per **@value**:  
  
    -   **0** : il filtro dell'articolo è statico oppure non restituisce un subset univoco di dati per ogni partizione, ovvero si tratta di una partizione "sovrapposta".  
  
    -   **1** : le partizioni risultanti sono sovrapposte e gli aggiornamenti apportati nel Sottoscrittore non possono modificare la partizione a cui appartiene una riga.  
  
    -   **2** : il filtro dell'articolo restituisce partizioni non sovrapposte, ma più Sottoscrittori ricevono la stessa partizione.  
  
    -   **3** : il filtro dell'articolo restituisce partizioni non sovrapposte univoche per ogni sottoscrizione.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 In questo esempio viene definito un gruppo di articoli di una pubblicazione di tipo merge in cui agli articoli è applicata una serie di filtri di join sulla tabella `Employee` che presenta essa stessa un filtro di riga con parametri sulla colonna **LoginID** . Durante la sincronizzazione viene sostituito il valore restituito dalla funzione [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) . Per altre informazioni, vedere la sezione relativa alla sostituzione del valore HOST_NAME() nell'argomento [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Modificare le proprietà di pubblicazioni e articoli](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
