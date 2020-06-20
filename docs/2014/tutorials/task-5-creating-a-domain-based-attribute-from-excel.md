---
title: 'Attività 5: creazione di un attributo basato su dominio da Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6f7287091ddd64ef9df1c63706a2f562feed4a5d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999665"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Attività 5: Creazione di un attributo basato su dominio di Excel
  In questa attività viene convertito l'attributo **state** dell'entità **Supplier** come **attributo basato su dominio**. Dopo aver configurato l'attributo State in modo che sia basato su dominio e pubblicato in MDS, viene creata una nuova entità denominata **state** nel server MDS con tutti i valori nella colonna e l'attributo **state** dell'entità **Supplier** verrà popolato con i valori dell'entità **state** . A questo punto, il modello **Suppliers** deve avere due entità: **Supplier** e **state** , dove l'attributo **state** dell'entità **Supplier** è un attributo basato su dominio che dipende dall'entità **state** .  
  
1.  Passa alla finestra di **Excel** con **Suppliers.xlsxpuliti e corrispondenti** aperti.  
  
2.  Fare clic sul pulsante **Aggiorna** sulla barra multifunzione per ottenere gli aggiornamenti più recenti da MDS. Verranno visualizzati i due record più se è stata eseguita l'attività facoltativa **4**.  
  
3.  Fare clic su **stato** nome colonna (cella **I1**) nella **riga di intestazione**.  
  
     ![Excel - Pulsante Proprietà attributi](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - Pulsante Proprietà attributi")  
  
4.  Fare clic su **Proprietà attributo** sulla barra multifunzione.  
  
5.  Nella finestra di dialogo **Proprietà attributo** selezionare **elenco vincolato (basato su dominio)** per il tipo di **attributo**.  
  
6.  Digitare **state** per il **nome della nuova entità** e fare clic su **OK**.  
  
     ![Excel - Finestra di dialogo Proprietà attributi](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - Finestra di dialogo Proprietà attributi")  
  
7.  A questo punto, in Excel dovrebbe essere visualizzata la **freccia in giù** quando si fa clic su qualsiasi valore nella colonna **stato** . Se necessario, il valore può essere modificato utilizzando l'elenco a discesa.  
  
     ![Excel - Elenco a discesa con gli Stati](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - Elenco a discesa con gli Stati")  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 6: Verifica della creazione dell'attributo basato su dominio tramite Gestione dati master](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
