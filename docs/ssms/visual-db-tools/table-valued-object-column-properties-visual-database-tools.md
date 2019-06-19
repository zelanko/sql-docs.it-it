---
title: Proprietà dell'oggetto con valori di tabella (colonna) (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 28cb15b30f838f3acb1cb097f751b0f60de7ca52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098044"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>Proprietà colonna dell'oggetto valutato a livello di tabella (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Queste proprietà vengono visualizzate quando si seleziona una colonna in un oggetto con valori di tabella nel riquadro **Diagramma** di Progettazione query e Progettazione viste.  
  
> [!NOTE]  
> Le proprietà illustrate in questo argomento sono ordinate per categoria anziché alfabeticamente.  
  
> [!NOTE]  
> È possibile che le finestre di dialogo e i comandi di menu visualizzati varino da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa/Esporta impostazioni** dal menu **Strumenti** .  
  
**Categoria Identità**  
Espandere questa categoria per visualizzare la proprietà **Nome** .  
  
**Nome**  
Indica il nome della colonna selezionata.  
  
**Categoria Progettazione query**  
Espandere questa categoria per visualizzare le proprietà per **Consenti valori Null**, **Regole di confronto**, **Tipo di dati**, **Lunghezza**, **Precisione**, **Scala**e **Dimensione**.  
  
**Consenti valori Null**  
Indica se il tipo di dati della colonna accetta valori Null.  
  
**Regole di confronto**  
Indica l'impostazione delle regole di confronto per la colonna selezionata. È possibile impostare il confronto nella scheda Proprietà colonna di Progettazione tabelle.  
  
**Tipo di dati**  
Mostra il tipo di dati della colonna selezionata.  
  
**Lunghezza**  
Indica il numero di caratteri o cifre consentiti dal tipo di dati della colonna selezionata. Questa proprietà è disponibile solo per tipi di dati basati su caratteri.  
  
> [!NOTE]  
> Per le dimensioni in byte, vedere la proprietà **Dimensione** di seguito.  
  
**Precisione**  
Indica il numero massimo di cifre ammesse per i tipi di dati numerici. Questa proprietà corrisponde a **0** per i tipi di dati non numerici.  
  
**Scala**  
Indica il numero massimo di cifre ammesse dopo la virgola decimale nei tipi di dati numerici. Questo valore deve essere inferiore o uguale al valore di precisione. Questa proprietà corrisponde a **0** per i tipi di dati non numerici.  
  
**Dimensione**  
Indica la dimensione in byte consentita dal tipo di dati della colonna. Ad esempio, un tipo di dati nchar può avere una lunghezza di 10 (il numero di caratteri), ma avrebbe una dimensione di 20 per quanto riguarda i set di caratteri Unicode.  
  
