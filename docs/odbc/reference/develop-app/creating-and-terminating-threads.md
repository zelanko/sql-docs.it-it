---
description: Creazione e interruzione di thread
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0100b85bc596149d809dee7e6c4cb3547dbd081
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465853"
---
# <a name="creating-and-terminating-threads"></a>Creazione e interruzione di thread
Le applicazioni multithread che utilizzano ODBC devono chiamare Microsoft® Visual C++® funzioni della libreria di runtime **_beginthread** e **_endthread** (o **_beginthreadex** e **_endthreadex**) per creare e terminare i thread che chiamano Gestione driver ODBC. Se le applicazioni chiamano le funzioni di® di Microsoft Windows NT **CreateThread** e **EndThread** , le perdite di memoria si verificheranno perché Gestione driver e alcuni driver ODBC chiamano funzioni di runtime C che non funzioneranno in un thread creato chiamando **CreateThread**. Per ulteriori informazioni, vedere la documentazione di Microsoft Windows®.
