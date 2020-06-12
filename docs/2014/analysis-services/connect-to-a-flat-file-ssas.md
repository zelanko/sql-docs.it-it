---
title: Connettersi a un file flat (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connflatfile.f1
ms.assetid: a365991e-eded-4cd8-89c0-0daf6d658d15
author: minewiskan
ms.author: owend
ms.openlocfilehash: 970a55b709e164da573fbd224c13cc641a3ba06a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527197"
---
# <a name="connect-to-a-flat-file-ssas"></a>Connessione a un file flat (SSAS)
  Questa pagina dell' **Importazione guidata tabella** consente di connettersi a un file flat (con estensione txt), a un file con valori delimitati da tabulazioni (con estensione tab) o a un file con valori delimitati da virgole (con estensione csv). Per accedere alla procedura guidata da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], dal menu **Modello** selezionare **Importa da origine dati**.  
  
 Per connettersi a un file flat, è necessario che nel computer sia installato il provider ACE. Per altre informazioni, vedere [Origini dati supportate &#40;SSAS tabulare&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
> [!NOTE]  
>  Le credenziali dell'utente corrente vengono utilizzate in caso di selezione di un file in questa pagina. Tuttavia, l'importazione non verrà completata se l'utente specificato nella pagina Impostazioni di rappresentazione non dispone di privilegi sufficienti per leggere dal file selezionato.  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 **Nome descrittivo connessione**  
 Digitare un nome univoco per questa connessione all'origine dati. Questo campo è obbligatorio.  
  
 **Percorso file**  
 Specificare un percorso completo per il file.  
  
 **Sfoglia**  
 Selezionare il percorso in cui è disponibile un file.  
  
 **Separatore colonne**  
 Selezionare i separatori di colonna disponibili da un apposito elenco. Scegliere un separatore che non sia già presente nel testo.  
  
|Valore|Description|  
|-----------|-----------------|  
|Tabulazione (t)|Le colonne sono separate da un carattere di tabulazione (t).|  
|Virgola (,)|Le colonne sono separate da una virgola (,).|  
|Punto e virgola (;)|Le colonne sono separate da un punto e virgola (;).|  
|Spazio ( )|Le colonne sono separate da uno spazio ( ).|  
|Due punti (:)|Le colonne sono separate da due punti (:).|  
|Barra verticale (&#124;)|Le colonne sono separate da una barra verticale (&#124;).|  
  
 **Avanzate**  
 Specificare la codifica e le opzioni delle impostazioni locali per il file flat.  
  
 **Utilizza la prima riga per le intestazioni di colonna**  
 Specificare se utilizzare la prima riga di dati per le intestazioni di colonna della tabella di destinazione.  
  
 **Anteprima dati**  
 Consente di visualizzare in anteprima i dati nel file selezionato e di utilizzare le opzioni seguenti per modificare l'importazione dei dati.  
  
> [!NOTE]  
>  Solo le prime 50 righe nel file vengono visualizzate in questa anteprima.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Casella di controllo nell'intestazione di colonna**|Selezionare la casella di controllo per includere la colonna nell'importazione dei dati. Deselezionare la casella di controllo per rimuovere la colonna dall'importazione dei dati.|  
|**Pulsante freccia in giù nell'intestazione di colonna**|Consente di ordinare e filtrare i dati nella colonna.|  
  
 **Cancella filtri di riga**  
 Consente di rimuovere tutti i filtri applicati ai dati nelle colonne.  
  
  
