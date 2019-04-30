---
title: 'Attività 5: Creazione di un attributo basato su dominio da Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 1a2826bb0c9b542837e05b7f600c9ce7d934fd4e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63143078"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>Attività 5: Creazione di un attributo basato su dominio di Excel
  In questa attività si converte il **lo stato** attributo delle **Supplier** entità sotto forma di un **attributo basato su dominio**. Dopo aver configurato l'attributo State da uno basato su dominio e pubblicarlo in MDS, una nuova entità denominata **lo stato** verrà creato nel server MDS con tutti i valori nella colonna e il **stato** attributo del **Supplier** entità verrà popolato con i valori di **stato** entità. A questo punto, il **Suppliers** modello deve disporre di due entità: **Supplier** e **stato** in cui il **stato** attributo del **Supplier** entità è un attributo basato su dominio che dipende da **stato** entità.  
  
1.  Passare a **Excel** finestra dotata **Cleansed and Matched Suppliers. xlsx** aprire.  
  
2.  Fare clic su **Aggiorna** pulsante della barra multifunzione per ottenere gli aggiornamenti più recenti da MDS. Si dovrebbe vedere altri due record se è stata eseguita l'opzione facoltativa **attività 4**.  
  
3.  Fare clic sul nome della colonna **lo stato** (cella **I1**) nella **riga intestazione**.  
  
     ![Excel - pulsante Proprietà attributi](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - pulsante Proprietà attributi")  
  
4.  Fare clic su **delle proprietà degli attributi** sulla barra multifunzione.  
  
5.  Nel **delle proprietà degli attributi** finestra di dialogo **elenco vincolato (basato su dominio)** per il **tipo di attributo**.  
  
6.  Tipo di **lo stato** per il **Nome nuova entità** e fare clic su **OK**.  
  
     ![Excel - finestra di dialogo Proprietà attributi](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - finestra di dialogo Proprietà attributo")  
  
7.  A questo punto, in Excel, dovrebbe **freccia giù** quando si fa clic su qualsiasi valore nel **stato** colonna. Se necessario, il valore può essere modificato utilizzando l'elenco a discesa.  
  
     ![Excel - elenco a discesa elenco con gli stati](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - elenco a discesa elenco con gli Stati")  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 6: Verificare che l'attributo basato su dominio viene creato tramite Gestione dati Master](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
