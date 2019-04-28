---
title: Confronto di dati stringa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7fe9955ba4f20c4a20e24d99924adce7ff0d992a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828144"
---
# <a name="comparing-string-data"></a>confronto di dati stringa
  Il confronto tra stringhe costituisce una parte importante di molte delle trasformazioni eseguite da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e viene utilizzato anche nella valutazione di espressioni in variabili ed espressioni di proprietà. La trasformazione Ordinamento, ad esempio, confronta i valori in un set di dati per disporre i dati in ordine crescente o decrescente.  
  
## <a name="configuring-transformations-for-string-comparisons"></a>Configurazione di trasformazioni per i confronti di stringhe  
 Le trasformazioni Ordinamento, Aggregazione, Raggruppamento fuzzy e Ricerca fuzzy possono essere personalizzate modificando la modalità di confronto delle stringhe a livello di colonna. È ad esempio possibile specificare di ignorare maiuscole e minuscole nel confronto, ovvero considerare identici i caratteri maiuscoli e minuscoli.  
  
 Le trasformazioni seguenti utilizzano espressioni che possono includere confronti tra stringhe.  
  
-   La trasformazione Suddivisione condizionale può utilizzare confronti tra stringhe nelle espressioni per determinare a quale output inviare le righe di dati. Per altre informazioni, vedere [Trasformazione Suddivisione condizionale](transformations/conditional-split-transformation.md).  
  
-   La trasformazione Colonna derivata può utilizzare confronti tra stringhe nelle espressioni per generare nuovi valori di colonna. Per altre informazioni, vedere [Trasformazione Colonna derivata](transformations/derived-column-transformation.md).  
  
 Anche le variabili, i mapping di variabili e i vincoli di precedenza utilizzano espressioni, che possono includere confronti tra stringhe. Per altre informazioni sulle espressioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md).  
  
## <a name="processing-during-string-comparison"></a>Elaborazione durante il confronto di stringhe  
 A seconda dei dati e della configurazione della trasformazione, durante il confronto dei dati stringa è possibile eseguire le operazioni di elaborazione seguenti:  
  
-   Conversione dei dati in formato Unicode. Se i dati dell'origine non sono già in formato Unicode, verranno automaticamente convertiti in tale formato prima dell'esecuzione del confronto.  
  
-   Utilizzo delle impostazioni locali per applicare regole specifiche della lingua per l'interpretazione del tipo di ordinamento e dei valori di data, ora e decimali.  
  
-   Applicazione di opzioni di confronto a livello di colonna per definire la distinzione tra maiuscole e minuscole per i confronti.  
  
## <a name="converting-string-data-to-unicode"></a>Conversione di dati stringa in formato Unicode  
 A seconda della configurazione e delle operazioni eseguite da una trasformazione, i dati stringa possono essere convertiti nel tipo di dati DT_WSTR, ovvero una rappresentazione Unicode dei caratteri delle stringhe.  
  
 I dati stringa con il tipo di dati DT_STR vengono convertiti in Unicode utilizzando la tabella codici della colonna. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supporta le tabelle codici a livello di colonna e ogni colonna può essere convertita usando una tabella codici diversa.  
  
 Nella maggior parte dei casi [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è in grado di identificare la tabella codici appropriata basandosi sull'origine dati. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio, è possibile impostare regole di confronto a livello di database e di colonna. La tabella codici viene ricavata dalle regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che possono essere quelle di Windows o le regole di confronto SQL.  
  
 Se in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene specificata una tabella codici imprevista oppure se tramite il pacchetto viene effettuato l'accesso a un'origine dati usando un provider da cui non vengono fornite informazioni sufficienti per determinare la tabella codici appropriata, è possibile specificare una tabella codici predefinita nell'origine e nella destinazione OLE DB. Le tabelle codici predefinite vengono utilizzate al posto di quelle specificate da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 I file non hanno tabelle codici, ma le gestioni connessioni file flat e per più file flat utilizzate dai pacchetti per connettersi ai file includono una proprietà che consente di specificare le tabelle codici dei file. La tabella codici può essere impostata solo a livello di file, non a livello di colonna.  
  
## <a name="setting-locale"></a>Impostazione delle impostazioni locali  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non usa la tabella codici per ricavare regole specifiche delle impostazioni locali per l'ordinamento dei dati o l'interpretazione di valori di data, ora e decimali. La trasformazione legge invece le impostazioni locali specificate dalla proprietà LocaleId del componente del flusso di dati, dell'attività Flusso di dati, del contenitore o del pacchetto. Per impostazione predefinita, le impostazioni locali di una trasformazione vengono ereditate dalla relativa attività Flusso di dati, che a sua volta le eredita dal pacchetto. Se l'attività Flusso di dati si trova in un contenitore, ad esempio Ciclo For, erediterà le impostazioni locali dal contenitore.  
  
 È inoltre possibile specificare impostazioni locali per le gestioni connessioni file flat e per più file flat.  
  
## <a name="setting-comparison-options"></a>Impostazione delle opzioni di confronto  
 Le impostazioni locali specificano le regole di base per il confronto dei dati stringa, ad esempio la posizione di ogni lettera nell'alfabeto. Tali regole possono tuttavia non essere sufficienti per i confronti eseguiti da alcune trasformazioni e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supporta un set di opzioni di confronto avanzate che consentono di eseguire confronti più specifici di quelli previsti dalle regole di confronto delle impostazioni locali. Tali opzioni di confronto vengono impostate a livello di colonna. È ad esempio disponibile un'opzione di confronto che consente di ignorare i caratteri senza spaziatura. L'effetto di questa opzione è per ignorare i segni diacritici, ad esempio la distinzione tra caratteri accentati, che rende "a" e "å" identici per il confronto.  
  
 Nella tabella seguente vengono descritte le opzioni di confronto disponibili e uno stile di ordinamento.  
  
|Opzione di confronto|Descrizione|  
|-----------------------|-----------------|  
|Ignora maiuscole/minuscole|Specifica se nel confronto viene fatta distinzione tra lettere maiuscole e minuscole. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la combinazione di maiuscole e minuscole. Ad esempio, la stringa "ABC" verrà considerata identica alla stringa "abc".|  
|Ignora Katakana/Hiragana|Specifica se nel confronto viene fatta distinzione tra i due tipi di caratteri Kana giapponesi, Hiragana e Katakana. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la distinzione tra Katakana e Hiragana.|  
|Ignora larghezza caratteri|Specifica se nel confronto viene fatta distinzione tra un carattere a un byte (metà larghezza) e lo stesso carattere rappresentato con due byte (larghezza intera). Se questa opzione è impostata, nel confronto tra stringhe la rappresentazione a un byte e quella a due byte dello stesso carattere verranno considerate uguali.|  
|Ignora caratteri senza spaziatura|Specifica se nel confronto viene fatta distinzione tra i caratteri con spaziatura e quelli con segni diacritici. Se questa opzione è impostata, nel confronto verranno ignorati i segni diacritici. Ad esempio, il carattere "å" verrà considerato uguale al carattere "a".|  
|Ignora simboli|Specifica se nel confronto viene fatta distinzione tra lettere e simboli, ad esempio gli spazi, i segni di punteggiatura, i simboli di valuta e i simboli matematici. Se questa opzione è impostata, nel confronto verranno ignorati i simboli. Ad esempio, la stringa " New York" verrà considerata identica alla stringa "New York" e la stringa "*ABC" verrà considerata identica alla stringa "ABC"'.|  
|Ordina i segni di punteggiatura come simboli|Specifica se nel confronto tutti i segni di punteggiatura, ad eccezione del segno meno e dell'apostrofo, precedono i caratteri alfanumerici. Ad esempio, se questa opzione è impostata la stringa ".ABC" precederà la stringa "ABC".|  
  
 Le trasformazioni Ordinamento, Aggregazione, Raggruppamento fuzzy e Ricerca fuzzy includono queste opzioni per il confronto dei dati.  
  
 Nella finestra **Editor avanzato** per le trasformazioni Raggruppamento fuzzy e Ricerca fuzzy è visualizzato il flag di confronto **FullySensitive** . Se si seleziona il flag di confronto **FullySensitive** vengono applicate tutte le opzioni di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di Integration Services](integration-services-data-types.md)   
 [Analisi veloce](../fast-parse.md)   
 [Analisi standard](../standard-parse.md)  
  
  
