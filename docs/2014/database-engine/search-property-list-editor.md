---
title: Editor elenco proprietà di ricerca | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.searchpropertylisteditor.f1
ms.assetid: 0f3ced6e-0dfd-49fc-b175-82378c3d668e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c68ec986e2c6f4f53dfec7f188ba2a120532ae4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929302"
---
# <a name="search-property-list-editor"></a>Editor dell'elenco delle proprietà di ricerca
  Utilizzare questa finestra di dialogo per aggiungere o eliminare proprietà di ricerca in un elenco di proprietà di ricerca.  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>Per utilizzare SQL Server Management Studio per gestire gli elenchi di proprietà di ricerca  
 Per informazioni sulla creazione, la visualizzazione o l'eliminazione di un elenco di proprietà di ricerca e sulla configurazione di un indice full-text per la ricerca di proprietà, vedere la pagina relativa alla [ricerca delle proprietà dei documenti con gli elenchi delle proprietà di ricerca](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="options"></a>Opzioni  
 **Nome proprietà**  
 Specificare il nome da utilizzare per identificare la proprietà nelle query full-text. Un nome di proprietà può contenere spazi interni. La lunghezza massima consentita per **Nome proprietà** è 256 caratteri. Questo nome può essere un nome descrittivo, ad esempio "Autore" o "Indirizzo abitazione" oppure il nome canonico Windows della proprietà, ad esempio `System.Author` o `System.Contact.HomeAddress`. **Nome proprietà** deve identificare in modo univoco la proprietà all'interno del set di proprietà.  
  
 Gli sviluppatori utilizzano il nome della proprietà per identificare la proprietà nel predicato [CONTAINS](/sql/t-sql/queries/contains-transact-sql) . Quando si aggiunge una proprietà è pertanto importante specificare un valore che la rappresenti in modo significativo.  
  
 **GUID set di proprietà**  
 Consente di specificare l'identificatore del set di proprietà a cui appartiene la proprietà. Si tratta di un identificatore univoco globale (GUID, Globally Unique Identifier). Un set di proprietà è un gruppo di proprietà correlate logicamente. Per informazioni sull'acquisizione di questo valore, vedere la sezione "Osservazioni" più avanti in questo argomento.  
  
 **ID interno proprietà**  
 Consente di specificare un identificatore di tipo integer per la proprietà. Questo valore pre-assegnato è un numero intero positivo univoco all'interno del set di proprietà. Per informazioni sull'acquisizione di questo valore, vedere la sezione "Osservazioni" più avanti in questo argomento.  
  
> [!NOTE]  
>  Le proprietà documento in cui vengono utilizzati identificatori stringa non sono supportate dalla ricerca full-text.  
  
 **Descrizione proprietà**  
 Se lo si desidera, è possibile specificare una descrizione per la proprietà. Si tratta di una stringa composta da un massimo di 512 caratteri. Una descrizione può ad esempio contenere informazioni sul set di proprietà della proprietà stessa oppure informazioni su una proprietà che non è possibile dedurre dal nome.  
  
## <a name="remarks"></a>Commenti  
 Per aggiungere una proprietà di ricerca a un elenco di proprietà di ricerca, è necessario specificare l'identificatore univoco globale (GUID) del set di proprietà a cui appartiene la proprietà e l'identificatore di tipo integer della proprietà. Una combinazione specifica di questi elementi deve essere univoca in un determinato elenco di proprietà di ricerca. Se si tenta di aggiungere una combinazione esistente, l'operazione ha esito negativo e viene restituito un errore. Ciò significa che è possibile configurare un solo nome per una proprietà specifica.  
  
 La descrizione della proprietà è facoltativa.  
  
 **Per configurare un elenco di proprietà di ricerca per un indice full-text**  
  
-   [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
## <a name="permissions"></a>Autorizzazioni  
 Vedere l' [elenco delle proprietà ALTER SEARCH &#40;&#41;Transact-SQL ](/sql/t-sql/statements/alter-search-property-list-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)   
 [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
