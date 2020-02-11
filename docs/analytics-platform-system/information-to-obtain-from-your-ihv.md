---
title: Ottenere informazioni da IHV
description: Informazioni da ottenere dalla IHV sull'appliance del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 730cf09ab7e45ea74070db591592fdb871243a77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401060"
---
# <a name="information-to-obtain-from-your-ihv"></a>Informazioni da ottenere dalla IHV
Quando il fornitore dell'hardware indipendente (IHV) recapita la nuova appliance di SQL Server PDW all'utente, fornirà anche informazioni sull'hardware del dispositivo e sulla configurazione eseguita nell'appliance. Queste informazioni sono necessarie per amministrare il dispositivo.  
  
L'elenco seguente mostra le informazioni che sono in genere necessarie per la IHV. In alcuni casi sono necessarie informazioni aggiuntive o aggiuntive. Verificare con il IHV per assicurarsi che tutte le informazioni rilevanti siano state trasferite all'utente con il recapito dell'appliance.  
  
|||  
|-|-|  
|**Informazioni o documento**|**Descrizione**|  
|Distinta base (BOM)|La fattura dei materiali elenca i componenti inclusi nell'appliance. Queste informazioni sono necessarie per confermare che tutti i componenti sono stati recapitati.<br /><br />**Importante:** La distinta base deve includere i pesi per ogni nodo del dispositivo e per ogni rack completo. Queste informazioni sono importanti quando si pianifica come gestire e spostare i componenti dell'appliance e per assicurarsi che il data center possa adattarsi al dispositivo. Se il BOM non include i pesi del nodo, assicurarsi di ottenere queste informazioni dalla IHV per tutti i nodi.|  
|Diagrammi di cablaggio|I diagrammi di cablaggio mostrano come connettere la rete, la potenza e altri cavi per ogni rack dell'appliance. Questi diagrammi sono necessari quando si installa il dispositivo nel data center e ogni volta che è necessario rimuovere o sostituire un componente.|  
|Requisiti per il racking degli appliance|Prima di poter installare il dispositivo nella data center, è necessario verificare se il data center soddisfa i requisiti di flusso d'aria e di lunghezza del cavo per l'appliance, nonché le dimensioni e i requisiti di alimentazione per i componenti. Vedere anche la distinta base (BOM) per informazioni sui pesi dei componenti dell'appliance, che è necessario anche.|  
  
