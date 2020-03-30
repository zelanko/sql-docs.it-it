---
title: Finestra di dialogo Apri file
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vs.openfile
ms.assetid: 3e01b9f5-2b0a-4fb3-9da8-984d27d17b8a
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 61a0a699c7d754d3b21b671da5cd29ea0ec0f240
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75251461"
---
# <a name="open-file-dialog-box"></a>Finestra di dialogo Apri file
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Usare la finestra di dialogo **Apri file** per aprire un file esistente sul disco. o per aprire un file già aperto utilizzando opzioni di codifica della lingua diverse.  
  
Per accedere a questa finestra di dialogo, selezionare **Apri** dal menu **File** e scegliere **File**. Questa finestra di dialogo viene visualizzata anche quando si aprono file da altri elementi, ad esempio dalla finestra di dialogo **Strumenti esterni** . Per aprire la finestra di dialogo simile **Apri progetto** , scegliere **Apri**dal menu **File** e selezionare **Progetto/Soluzione** .  
  
> [!NOTE]  
> Prima di aprire un progetto o un componente in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], determinare l'affidabilità del relativo codice. L'apertura del progetto o del componente in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] potrebbe infatti causare l'esecuzione del codice in un processo trusted sul computer locale.  
  
## <a name="option"></a>Opzione  
**Look in**  
Consente di individuare la cartella progetto esistente utilizzando il menu a discesa. Selezionando una cartella in questo elenco viene visualizzato il contenuto della cartella nel riquadro principale.  
  
## <a name="my-places-bar"></a>Barra Risorse personali  
**Desktop**  
Consente di visualizzare i file e le cartelle che si trovano sul desktop.  
  
**Progetti**  
Visualizza i file e le cartelle nella cartella **Progetti** dell'utente.  
  
**Risorse del computer**  
Consente di visualizzare il contenuto del disco floppy, del disco rigido e dell'unità CD-ROM.  
  
## <a name="folder-list"></a>Elenco cartelle  
**Nome file**  
Questa opzione consente di applicare un filtro alle cartelle e ai file visualizzati. Immettere il nome completo o parziale del file in base al quale applicare il filtro. È possibile utilizzare l'asterisco (*) come carattere jolly.  
  
**Tipo file**  
Questa opzione consente di filtrare il contenuto della cartella o della directory selezionata in Cerca in per un particolare tipo di file.  
  
**Apri con e Opzioni di codifica**  
Per usare la **finestra di dialogo Apri con** in modo da poter specificare un editor per il file di destinazione, selezionare il rettangolino a destra del pulsante **Apri** e scegliere **Apri con**. Se necessario, è possibile specificare anche uno schema di codifica della lingua da applicare durante l'apertura del file selezionato. A tale scopo, nell'elenco selezionare un programma che contiene la definizione "**con codifica**" e scegliere **Apri** per visualizzare la **finestra di dialogo Codifica**. Pulsante non sempre disponibile.  
  
## <a name="toolbar"></a>Barra degli strumenti  
**Esplora indietro**  
Torna alla cartella, all'unità o all'indirizzo Internet visualizzati per ultimi.  
  
**Livello superiore**  
Esplora l'albero fino alla cartella immediatamente superiore nella visualizzazione albero.  
  
**Ricerca sul Web**  
Pulsante non disponibile.  
  
**Elimina**  
Elimina i file o le cartelle selezionati dalla relativa posizione di archiviazione.  
  
**Nuova cartella**  
Visualizza la finestra di dialogo **Nuova cartella** . Questa opzione consente di creare una nuova cartella figlio sotto la cartella selezionata nell'elenco a discesa **Cerca in** .  
  
## <a name="views"></a>Viste  
Include opzioni per la riorganizzazione e la visualizzazione del contenuto dell'elemento selezionato nell'elenco a discesa **Viste** .  
  
**Anteprima**  
Visualizza l'anteprima degli elementi contenuti nel riquadro di visualizzazione.  
  
**Titoli**  
Visualizza i file e le cartelle come icone grandi.  
  
**Icone**  
Visualizza i file e le cartelle come icone piccole.  
  
**Elenco**  
Visualizza i file e le cartelle in un formato a elenco.  
  
**Dettagli**  
Visualizza il nome, le dimensioni, il tipo e la data dell'ultima modifica di file e cartelle in un formato a elenco. Fare clic su un'intestazione di colonna per ordinare l'elenco in base a un particolare dettaglio.  
  
**WebView**  
Comando non disponibile.  
  
## <a name="tools"></a>Strumenti  
Selezionare uno strumento da applicare all'elemento selezionato nel riquadro del contenuto.  
  
**Elimina**  
Elimina il file o la cartella selezionati dalla relativa posizione di archiviazione.  
  
**Connetti unità di rete**  
Apre la finestra di dialogo **Connetti unità di rete** .  
