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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3536deef604d7dbf645903e7d171a58cd9fec96a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301692"
---
# <a name="creating-and-terminating-threads"></a>Creazione e interruzione di thread
Le applicazioni multithread che utilizzano ODBC devono chiamare Microsoft® Visual C++® funzioni della libreria di runtime **_beginthread** e **_endthread** (o **_beginthreadex** e **_endthreadex**) per creare e terminare i thread che chiamano Gestione driver ODBC. Se le applicazioni chiamano le funzioni di® di Microsoft Windows NT **CreateThread** e **EndThread** , le perdite di memoria si verificheranno perché Gestione driver e alcuni driver ODBC chiamano funzioni di runtime C che non funzioneranno in un thread creato chiamando **CreateThread**. Per ulteriori informazioni, vedere la documentazione di Microsoft Windows®.
