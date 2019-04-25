---
title: Creazione e interruzione di thread | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e9d6d15c449d88043e844addd12ac10a98d5c4a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470869"
---
# <a name="creating-and-terminating-threads"></a>Creazione e interruzione di thread
Applicazioni multithread che utilizzano ODBC devono chiamare il Microsoft® Visual C++® funzioni della libreria Run-Time **beginthread** e **endthread** (o **beginthreadex**e **endthreadex**) per creare e interrompere i thread che chiamano gestione Driver ODBC. Se le applicazioni chiamano le funzioni Microsoft Windows NT® **CreateThread** e **EndThread** invece funzioni perché Gestione Driver e alcuni driver ODBC chiamare run-time C si verificherà le perdite di memoria non verrà eseguito su un thread creato chiamando **CreateThread**. Per altre informazioni, vedere la documentazione Microsoft Windows®.
