---
title: Destinazione di File flessibili | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfiledest.f1
- sql14.dts.designer.afpextfiledest.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a0ffa4b881fe550aba6c547fcea690932eef110
ms.sourcegitcommit: fa2afe8e6aec51e295f55f8cc6ad3e7c6b52e042
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/03/2019
ms.locfileid: "66462621"
---
# <a name="flexible-file-destination"></a>Destinazione di File flessibili

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Il componente **Destinazione di File flessibili** consente a un pacchetto SSIS di scrivere dati in vari servizi di archiviazione supportati.

I servizi di archiviazione attualmente supportati sono:

- [Archiviazione BLOB di Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
   
Trascinare e rilasciare **Destinazione di File flessibili** nella finestra di progettazione del flusso di dati e fare doppio clic su di esso per visualizzare l'editor.
  
**Destinazione di File flessibili** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

Le seguenti proprietà sono disponibili nell'**Editor Destinazione di File flessibili**.

- **Tipo di gestione connessione file:** specifica il tipo di gestione connessione di origine. Sceglierne una esistente del tipo specificato oppure crearne una nuova.
- **Percorso cartella:** specifica il percorso della cartella di destinazione.
- **Nome file:** specifica il nome file di destinazione.
- **Formato di file:** specifica il formato del file di destinazione. I formati supportati sono **Testo**, **Avro**, **ORC**, **Parquet**.
- **Carattere delimitatore di colonna:** specifica il carattere da usare come delimitatore di colonna (i delimitatori composti da più caratteri non sono supportati).
- **Prima riga come nome di colonna:** specifica se scrivere i nomi di colonna nella prima riga.
- **Comprimi file:** specifica se comprimere il file.
- **Tipo di compressione:** specifica il formato di compressione da usare. I formati supportati sono **GZIP**, **DEFLATE**, **BZIP2**.
- **Livello di compressione:** specifica il livello di compressione da usare.

Le seguenti proprietà sono disponibili nell'**Editor avanzato**.

- **rowDelimiter:** carattere usato per separare le righe in un file. È consentito un solo carattere. Il valore **predefinito** è \r\n.
- **escapeChar:** carattere speciale usato per eseguire l'escape di un delimitatore di colonna nel contenuto del file di input. Non è possibile specificare sia escapeChar sia quoteChar per una tabella. È consentito un solo carattere. Nessun valore predefinito.
- **quoteChar:** carattere usato per inserire un valore stringa tra virgolette. I delimitatori di riga e colonna all'interno delle virgolette sono considerati come parte del valore della stringa. Questa proprietà è applicabile ai set di dati di input e di output. Non è possibile specificare sia escapeChar sia quoteChar per una tabella. È consentito un solo carattere. Nessun valore predefinito.
- **nullValue:** uno o più caratteri usati per rappresentare un valore null. Il valore **predefinito** è \N.
- **encodingName:** specifica il nome della codifica. Vedere la proprietà [Encoding.EncodingName](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8).
- **skipLineCount:**  indica il numero di righe non vuote da ignorare durante la lettura dei dati dai file di input. Se vengono specificati sia skipLineCount che firstRowAsHeader, le righe vengono ignorate e quindi le informazioni dell'intestazione vengono lette dal file di input.
- **treatEmptyAsNull:** specifica se considerare una stringa null o vuota come valore null durante la lettura dei dati da un file di input. Il valore **predefinito** è True.

Dopo aver specificato le informazioni di connessione, passare alla pagina **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione per il flusso di dati SSIS.

**Prerequisiti per il formato di file ORC/Parquet**

Per usare il formato di file ORC/Parquet è necessario Java.
L'architettura (a 32 o a 64 bit) della build di Java deve corrispondere a quella del runtime di SSIS da usare.
Sono state sottoposte a test le build di Java seguenti.

- [OpenJDK 8u192 di Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

**Configurare OpenJDK di Zulu**

1. Scaricare ed estrarre il pacchetto di installazione con estensione zip.
2. Dal prompt dei comandi, eseguire `sysdm.cpl`.
3. Nella scheda **Avanzate** selezionare **Variabili di ambiente**.
4. Nella sezione **Variabili di sistema** selezionare **Nuova**.
5. Immettere `JAVA_HOME` in **Nome variabile**.
6. Selezionare **Sfoglia directory**, passare alla cartella estratta e selezionare la sottocartella `jre`.
   Selezionare quindi **OK** e **Valore variabile** verrà popolato automaticamente.
7. Selezionare **OK** per chiudere la finestra di dialogo **Nuova variabile di sistema**.
8. Selezionare **OK** per chiudere la finestra di dialogo **Variabili di ambiente**.
9. Selezionare **OK** per chiudere la finestra di dialogo **Proprietà del sistema**.

**Configurare Oracle Java SE Runtime Environment**

1. Scaricare ed eseguire il programma di installazione con estensione exe.
2. Seguire le istruzioni del programma di installazione per completare l'installazione.
