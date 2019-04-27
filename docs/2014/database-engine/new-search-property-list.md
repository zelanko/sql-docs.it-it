---
title: Nuovo elenco di proprietà di ricerca | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.newsearchpropertylist.f1
ms.assetid: ffca78e9-8608-4b15-bd38-b2d78da4247a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2aff15a42c8bffeb5a54e92b9ce7a09ace282ce4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774502"
---
# <a name="new-search-property-list"></a>Nuovo elenco di proprietà di ricerca
  Utilizzare questa finestra di dialogo per creare un elenco di proprietà di ricerca.  
  
## <a name="options"></a>Opzioni  
 **Nome elenco di proprietà di ricerca**  
 Immettere il nome dell'elenco di proprietà di ricerca.  
  
 **Proprietario**  
 Consente di specificare il proprietario dell'elenco di proprietà di ricerca. Se si desidera impostare se stessi, ovvero l'utente corrente, come proprietario, lasciare vuoto questo campo. Per specificare un utente diverso, fare clic sul pulsante Sfoglia.  
  
### <a name="create-search-property-list-options"></a>Opzioni per la creazione di un elenco di proprietà di ricerca  
 Selezionare una delle opzioni seguenti:  
  
 **Crea un elenco di proprietà di ricerca vuoto**  
 Consente di creare un elenco di proprietà di ricerca senza proprietà.  
  
 **Crea da un elenco di proprietà di ricerca esistente**  
 Consente di copiare le proprietà di un elenco di proprietà di ricerca esistente nel nuovo elenco di proprietà. Gli elenchi di proprietà di ricerca sono oggetti di database, pertanto è necessario specificare il database contenente l'elenco di proprietà che si desidera copiare.  
  
 **Database di origine**  
 Consente di specificare il nome del database a cui appartiene l'elenco di proprietà di ricerca esistente. Per impostazione predefinita, è selezionato il database corrente. Se lo si desidera, è possibile utilizzare la casella di riepilogo per selezionare un database diverso, se la connessione corrente è associata a un ID utente in tale database.  
  
 **Elenco di proprietà di ricerca di origine**  
 Selezionare il nome di un elenco di proprietà di ricerca esistente tra quelli che appartengono al database selezionato.  
  
## <a name="permissions"></a>Permissions  
 Visualizzare [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql).  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>Per utilizzare SQL Server Management Studio per gestire gli elenchi di proprietà di ricerca  
 Per informazioni su come creare, visualizzare, modificare o eliminare un elenco di proprietà di ricerca e su come configurare un indice full-text per la ricerca di proprietà, vedere [proprietà del documento di ricerca con elenchi delle proprietà di ricerca](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)   
 [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
