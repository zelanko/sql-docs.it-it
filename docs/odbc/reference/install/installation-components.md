---
description: Componenti di installazione
title: Componenti di installazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aac17b66b52b6d5b167f670302b8e1df14f8907a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499824"
---
# <a name="installation-components"></a>Componenti di installazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 Il processo di installazione viene avviato quando l'utente esegue il programma di installazione. Il programma di installazione funziona insieme alla *dll* del programma di installazione e a una *dll di installazione driver* per ogni driver. Sia il programma di installazione che la DLL del programma di installazione usano gli argomenti nelle funzioni **SQLInstallDriverEx** e **SQLInstallTranslatorEx** per determinare i file da copiare o eliminare per ogni componente. Nella figura seguente viene illustrata la relazione tra questi componenti di installazione.  
  
 ![Relazione tra componenti di installazione](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Il file ODBC. inf utilizzato in ODBC *2. x* per descrivere i file richiesti da ogni componente ODBC non viene utilizzato in ODBC *3. x*. I driver che inviano i componenti ODBC *3. x* non devono creare un file ODBC. inf. Il rendering di ODBC. inf non è necessario per la rimozione di **SQLInstallDriver** e **SQLInstallODBC**e per la deprecazione di **SQLInstallTranslator**. Le informazioni sul driver utilizzate nelle sezioni della parola chiave driver di ODBC. inf sono ora disponibili nell'argomento *lpszDriver* in **SQLInstallDriverEx**. Le informazioni di conversione che erano utilizzate nelle sezioni [ODBC Translator] e Translator Specification di ODBC. inf sono ora disponibili nell'argomento *lpszTranslator* di **SQLInstallTranslatorEx**. Queste modifiche consentono al programma di installazione ODBC di essere più portabile su più piattaforme.  
  
 Per ulteriori informazioni su questi componenti, vedere gli argomenti seguenti alla fine di questa sezione.  
  
-   [Programma di installazione](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL di installazione](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL di installazione driver](../../../odbc/reference/install/driver-setup-dll.md)
