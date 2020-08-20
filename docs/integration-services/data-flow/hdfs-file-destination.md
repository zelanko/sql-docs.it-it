---
description: Destinazione file HDFS
title: Destinazione file HDFS | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cfac02ca6db43d77f9157449df7319a6b67418e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477836"
---
# <a name="hdfs-file-destination"></a>Destinazione file HDFS

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Il componente Destinazione file HDFS consente a un pacchetto SSIS di scrivere dati in un file HDFS. I formati di file supportati sono testo, Avro e ORC.

 Per configurare Destinazione file HDFS, trascinare e rilasciare Origine file HDFS nella finestra di progettazione del flusso di dati e fare doppio clic sul componente per aprire l'editor.

 ![Editor destinazione file HDFS](../../integration-services/data-flow/media/hdfs-file-dest.png "Editor destinazione file HDFS")

## <a name="options"></a>Opzioni
 Configurare le opzioni seguenti nella scheda **Generale** della finestra di dialogo **Editor destinazione file HDFS** .

|Campo|Descrizione|
|-----------|-----------------|
|**Connessione Hadoop**|Specificare un'istanza esistente di Gestione connessione Hadoop o crearne una nuova. Questa istanza di Gestione connessione indica dove sono ospitati i file HDFS.|
|**Percorso file**|Specificare il nome del file HDFS.|
|**Formato file**|Specificare il formato del file HDFS. Le opzioni disponibili sono testo, Avro o ORC.|
|**Carattere delimitatore di colonna**|Se si seleziona il formato testo, specificare il carattere delimitatore di colonna.|
|**Nomi di colonna nella prima riga di dati**|Se si seleziona il formato testo, indicare se la prima riga del file contiene i nomi delle colonne.|

 Dopo aver configurato queste opzioni, selezionare la scheda **Colonne** per eseguire il mapping delle colonne di origine alle colonne di destinazione del flusso di dati.

::: moniker range=">= sql-server-ver15"

## <a name="prerequisite-for-orc-file-format"></a>Prerequisiti per il formato di file ORC
Per usare il formato di file ORC è necessario Java.
L'architettura (a 32 o a 64 bit) della build di Java deve corrispondere a quella del runtime di SSIS da usare.
Sono state sottoposte a test le build di Java seguenti.

- [OpenJDK 8u192 di Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Configurare OpenJDK di Zulu
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

### <a name="set-up-oracles-java-se-runtime-environment"></a>Configurare Oracle Java SE Runtime Environment
1. Scaricare ed eseguire il programma di installazione con estensione exe.
2. Seguire le istruzioni del programma di installazione per completare l'installazione.

::: moniker-end

## <a name="see-also"></a>Vedere anche
[Gestione connessione Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
[Origine file HDFS](../../integration-services/data-flow/hdfs-file-source.md)
