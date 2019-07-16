---
title: Ottenere le informazioni dal fornitore IHV - sistema di piattaforma Analitica | Microsoft Docs
description: Informazioni da ottenere dal fornitore IHV sull'appliance del sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 016a20567968e45456be79c8c67e77d7c3fbb2bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960831"
---
# <a name="information-to-obtain-from-your-ihv"></a>Informazioni da ottenere dal fornitore IHV
Quando il fornitore di hardware indipendenti (IHV) offre le nuove appliance di SQL Server PDW per l'utente, fornirà anche informazioni su hardware di appliance e la configurazione che hanno eseguito nell'appliance. È necessario che queste informazioni per amministrare il dispositivo.  
  
L'elenco seguente mostra le informazioni necessarie in genere dal fornitore IHV. In alcuni casi, sono necessarie informazioni aggiuntive o altri. Contattare il fornitore per assicurarsi che tutte le informazioni pertinenti sono state trasferite all'utente con il recapito di appliance.  
  
|||  
|-|-|  
|**Informazioni o documenti**|**Descrizione**|  
|Distinta base (BOM)|La distinta base sono elencati i componenti inclusi nell'appliance. Queste informazioni sono necessarie per verificare che tutti i componenti sono stati recapitati.<br /><br />**Importante:** Distinta dei materiali deve includere i pesi per ciascuno dei nodi di appliance e per ogni rack completo. Queste informazioni sono importanti quando si pianifica come gestire e spostare i componenti di appliance e per essere certi che il data center può gestire l'appliance. Se il carattere BOM non include i pesi dei nodi, assicurarsi di ottenere queste informazioni dal fornitore IHV per tutti i nodi.|  
|Cablaggio di diagrammi|Cablaggi diagrammi illustrano come connettersi la rete, alimentazione e altri cavi per ogni appliance rack. Questi diagrammi sono necessari quando si installa l'appliance nel data center e ogni volta che è necessario rimuovere o sostituire un componente.|  
|Requisiti scaffali Appliance|Prima di poter installare il dispositivo nel data center, è necessario sapere se il data center soddisfi i requisiti di power per i componenti e i requisiti di lunghezza dei cavi per l'appliance, nonché le dimensioni e il flusso d'aria. Vedere anche distinta base (BOM) sopra per informazioni sui valori di ponderazione componente appliance, anch ' esso necessari.|  
  
