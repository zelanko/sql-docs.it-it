---
title: Creare un attributo basato su dominio (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 09d0b3b339a70b5d2ccae3c9edca11ddf942e95c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65487590"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>Creare un attributo basato su dominio (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un attributo basato su dominio per popolare i valori di un attributo con i membri di un'entità.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   È necessario che un'entità esista perché venga utilizzata come origine dei valori di attributo. Ad esempio per creare un attributo basato su dominio che si basa sull'entità Color, è necessario prima creare l'entità Color. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
-   È necessario che sia presente un'entità perché ne venga creato l'attributo. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
## <a name="attribute-information"></a>Informazioni sugli attributi  
 Per ogni indice creato, viene aggiunta alla griglia una riga con sette colonne. La tabella seguente descrive le colonne.  
  
|colonna|Descrizione|  
|------------|-----------------|  
|Stato|Stato dell'attributo.<br /><br /> Quando si fa clic su Salva, viene visualizzata l'immagine ![Icona di aggiornamento dello stato](../master-data-services/media/mds-statusicon-updating.png "Icona di aggiornamento dello stato") che indica che è in corso l'aggiornamento dell'attributo.<br /><br /> Se si verificano errori durante la creazione o la modifica di un attributo viene visualizzata l'immagine ![Icona di errore](../master-data-services/media/mds-statusicon-error.png "Icona di errore").<br /><br /> In caso contrario lo stato è OK e viene visualizzata l'immagine ![Icona di stato OK](../master-data-services/media/mds-statusicon-ok.png "Icona di stato OK").|  
|Nome|Nome dell'attributo.|  
|Nome visualizzato|Nome visualizzato dell'attributo.|  
|Descrizione|Descrizione dell'attributo.|  
|Larghezza in pixel visualizzazione|Larghezza dell'attributo.|  
|Tipo e proprietà|Informazioni sul tipo e sul tipo di dati dell'attributo.|  
|Abilita rilevamento modifiche|Specifica se l'attributo è abilitato per il rilevamento delle modifiche e visualizza tra parentesi il numero del gruppo.|  
  
 Quando si fa clic su un attributo vengono visualizzate le informazioni seguenti.  
  
-   **Creato da**: nome dell'utente che ha creato l'attributo.  
  
-   **Il**: data e ora di creazione dell'attributo.  
  
-   **Aggiornato da**: nome dell'ultimo utente che ha aggiornato l'attributo.  
  
-   **Il**: data e ora dell'ultimo aggiornamento dell'attributo.  
  
### <a name="to-create-a-domain-based-attribute"></a>Per creare un attributo basato su dominio  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Gestione modelli** fare clic su un modello, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestisci entità** selezionare la riga dell'entità per la quale si vuole creare un attributo.  
  
4.  Fare clic su **Attributi**.  
  
5.  Nella pagina **Gestisci attributi** eseguire una di queste operazioni, quindi fare clic su **Aggiungi**.  
  
    -   Se l'attributo è per i membri foglia, selezionare **Foglia** nella casella di riepilogo **Tipo di membro** .  
  
    -   Se l'attributo è per i membri consolidati, selezionare **Consolidato** nella casella di riepilogo **Tipo di membro** .  
  
    -   Se l'attributo è per le raccolte, selezionare **Raccolta** nella casella di riepilogo **Tipo di membro** .  
  
6.  Nella casella **Nome** digitare un nome per l'attributo. Per un elenco di parole che non vanno usate come nomi di attributo, vedere [Parole riservate &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)  
  
7.  Facoltativamente, digitare un nome di visualizzazione e specificare una descrizione nella casella **Descrizione** .  
  
8.  Nella casella **Larghezza in pixel visualizzazione** digitare la larghezza della colonna attributo da visualizzare nella griglia **Esplora** .  
  
9. Nell'elenco **Tipo di attributo** selezionare **Basato su dominio**.  
  
10. Nell'elenco **Entità** scegliere l'entità da usare per popolare i valori dell'attributo. 
  
11. **Facoltativo, per attributi basati su dominio per i membri foglia.** Selezionare un attributo padre di filtro per vincolare i valori consentiti per l'attributo basato su dominio.  
  
     L'attributo padre di filtro deve essere un altro attributo basato su dominio per un membro foglia, all'interno della stessa entità. Deve essere presente una gerarchia derivata, con un livello che definisce la relazione padre-figlio tra le entità di dominio dei due attributi.  
  
     Per informazioni sull'applicazione di vincoli ai valori consentiti, vedere [How to filter Domain Based Attribute drop down lists](https://blogs.msdn.microsoft.com/mds/2015/12/03/in-sql-server-2016-master-data-services-how-to-filter-domain-based-attribute-drop-down-lists/)(Come filtrare gli elenchi a discesa di attributi basati sul dominio) nel blog Master Data Services.  
  
12. **Facoltativa.** Selezionare **Enable change tracking** per tenere traccia delle modifiche a gruppi di attributi. Per altre informazioni, vedere [Aggiungere attributi ad un gruppo rilevamento modifiche &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi basati su dominio &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [Creare una gerarchia derivata &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [Modificare il nome e il tipo di dati di un attributo &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Eliminare un attributo &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)  
  
  
