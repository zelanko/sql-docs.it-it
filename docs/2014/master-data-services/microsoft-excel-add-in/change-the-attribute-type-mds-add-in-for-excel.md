---
title: Modificare il tipo di attributo (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4406eb225002bbf5df93f8c67385694922d7d2c7
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482758"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>Modificare il tipo di attributo (componente aggiuntivo MDS per Excel)
  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]gli amministratori possono modificare il tipo di attributo quando il tipo di dati o il numero di caratteri consentiti non è corretto.  
  
 Per modificare il tipo di attributo per creare un elenco vincolato (attributo basato su dominio), vedere [Creare un attributo basato su dominio &#40;componente aggiuntivo MDS per Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  Non è possibile aggiornare il tipo o la lunghezza delle colonne **Nome** o **Codice**.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione di accesso alle aree funzionali **Amministrazione sistema** e **Visualizzatore** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   Devono essere disponibili un modello esistente, un'entità e un attributo.  
  
### <a name="to-change-the-attribute-type"></a>Per modificare il tipo di attributo  
  
1.  In Excel caricare l'entità contenente la colonna (attributo) che si desiderare modificare. Per altre informazioni, vedere [caricare i dati da MDS in Excel](export-data-to-excel-from-master-data-services.md).  
  
2.  Fare clic su una cella nella colonna che si desidera modificare.  
  
3.  Nel gruppo **Compila modello** fare clic su **Proprietà attributi**.  
  
4.  Nella finestra di dialogo **Proprietà attributi** aggiornare le impostazioni in base alle necessità.  
  
5.  Fare clic su **OK**.  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>Cosa accade quando si modifica il tipo di attributo  
 Se è presente una dipendenza dall'attributo, ad esempio all'attributo viene fatto riferimento da qualsiasi regola business MDS o l'attributo è incluso in una vista sottoscrizioni e si modifica il tipo di dati di un attributo, in MDS dovranno essere effettuate le seguenti operazioni:  
  
-   Modificare il tipo di dati dell'attributo.  
  
-   Generare una copia dell'attributo con il suffisso old"che non contiene alcun valore. Questa operazione viene definita un' **deprecato** attributo.  
  
 Tutte le dipendenze esistenti dall'attributo originale faranno tuttavia riferimento all'attributo deprecato e non a quello modificato.  
  
 Ciò implica quanto segue:  
  
-   È necessario aggiornare le regole business in modo che facciano riferimento all'attributo modificato, in quanto la logica potrebbe non essere la stessa applicata al nuovo tipo di dati dell'attributo. Sarà necessario modificare ogni regola interessata, quindi rielaborare le espressioni in modo che vengano rimossi i riferimenti dall'attributo deprecato (_old) e venga fatto riferimento all'attributo aggiornato.  
  
-   È necessario aprire tutte le viste sottoscrizioni nella selezione di Gestione integrazione, selezionare la riga della vista, aprirlo e modificarlo facendo clic sull'icona a forma di matita e quindi fare clic sui **salvataggio disco** icona per aggiornare la definizione della vista. Non sono necessarie altre modifiche per rigenerare la sintassi della vista.  
  
-   Alle tabelle di gestione temporanea che includono l'attributo verrà una colonna per l'attributo deprecato e ciò influirà sul codice di gestione temporanea. Per eliminare l'attributo deprecato, è possibile eliminarlo dopo avere aggiornato regole business e le viste sottoscrizioni.  
  
 **Eliminazione dell'attributo deprecato**  
  
 Prima di eliminare qualsiasi attributo deprecato, è necessario rimuovere tutti i riferimenti all'attributo, ad esempio correggere le regole business e rigenerare le viste sottoscrizioni come descritto in precedenza. In caso contrario, quando si tenta di eliminare l'attributo deprecato, verrà generato un errore nella pagina Web di amministrazione del sistema nel quale è indicato che l'attributo non può essere eliminato perché un oggetto fa riferimento a tale attributo.  
  
 Per eliminare un attributo, vedere [eliminazione di un attributo &#40;Master Data Services&#41;](../delete-an-attribute-master-data-services.md)  
  
> [!TIP]  
>  Modificare i tipi di dati per gli attributi MDS con dati esistenti ed entità correlate è un'operazione complessa, soprattutto se è presente una regola business o una vista sottoscrizioni dichiarata che dipende dall'entità. La procedura consigliata consiste nell'iniziare con un tipo di dati sufficientemente flessibile per contenere i valori necessari. Ad esempio, le stringhe potrebbero essere brevi inizialmente, ma con il tempo potrebbe essere necessario allungarle, quindi è consigliabile considerare il peggiore dei casi. Una lunghezza aggiuntiva della stringa di testo può essere gravosa, ad esempio le caselle di testo di grandi dimensioni della GUI sono difficili da adattare alla schermata, quindi è opportuno evitare stringhe troppo lunghe.  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi &#40;Master Data Services&#41;](../attributes-master-data-services.md)   
 [Compilazione di un modello &#40;componente aggiuntivo MDS per Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
