---
title: 'Attività 2: mapping delle colonne di Excel ai domini DQS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29d45e06dcd3e67af3abbc6b356d44877e40f46b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484698"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>Attività 2: Mapping delle colonne di Excel ai domini DQS
    
1.  Nella pagina **Mappa** selezionare **File di Excel** per **Origine dati**.  
  
2.  Fare clic su **Sfoglia**, selezionare **Suppliers. xlsx**, quindi fare clic su **Apri**.  
  
3.  Selezionare **IncomingSuppliers $** per il **foglio di foglio**.  
  
4.  Eseguire il mapping delle colonne come illustrato nella tabella e schermata seguenti. Quando si creano i mapping per il dominio di **stato** , fare clic sul pulsante **Aggiungi un mapping colonne** sulla barra degli strumenti posizionata sopra l'elenco.  
  
    > [!TIP]  
    >  Per la pulizia non si utilizza la colonna o il dominio **Supplier ID** . Il dominio **Supplier ID** viene usato più avanti nell'attività di corrispondenza.  
  
    |Colonna di Excel|Dominio DQS|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Indirizzo di posta elettronica del contatto|  
    |Riga indirizzo|Riga indirizzo|  
    |city|city|  
    |State|State|  
    |Country (fare clic su **+ (Aggiungi una colonna Mapping)** barra degli strumenti per aggiungere una riga|Country|  
    |Zip Code|Zip|  
  
     ![Mapping delle colonne di Excel ai domini](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Mapping delle colonne di Excel ai domini")  
  
5.  Poiché è stato eseguito il mapping di tutti i singoli domini all'interno del dominio composito **Address Validation** , il dominio composito partecipa automaticamente al processo di pulizia. Fare clic sul pulsante **Visualizza/Seleziona domini compositi** per verificare che il dominio composito **Address Validation** sia selezionato automaticamente, quindi fare clic su **OK**.  
  
     ![Finestra di dialogo Visualizza/Seleziona domini compositi](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "Finestra di dialogo Visualizza/Seleziona domini compositi")  
  
6.  Fare clic su **Avanti** per passare alla pagina **Pulisci** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 3: Pulizia dei dati fornitore rispetto alla Knowledge Base Suppliers](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
