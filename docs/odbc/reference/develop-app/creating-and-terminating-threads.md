---
title: Creazione e terminazione di thread | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002078"
---
# <a name="creating-and-terminating-threads"></a>Creazione e interruzione di thread
Le applicazioni multithread che utilizzano ODBC devono chiamare Microsoft® Visual C++® funzioni della libreria di runtime **_beginthread** e **_endthread** (o **_beginthreadex** e **_endthreadex**) per creare e terminare i thread che chiamano Gestione driver ODBC. Se le applicazioni chiamano le funzioni di® di Microsoft Windows NT **CreateThread** e **EndThread** , le perdite di memoria si verificheranno perché Gestione driver e alcuni driver ODBC chiamano funzioni di runtime C che non funzioneranno in un thread creato chiamando **CreateThread**. Per ulteriori informazioni, vedere la documentazione di Microsoft Windows®.
