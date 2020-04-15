---
title: Creazione e terminazione di thread Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301692"
---
# <a name="creating-and-terminating-threads"></a>Creazione e interruzione di thread
Le applicazioni multithread che utilizzano ODBC devono chiamare le funzioni della libreria di runtime di Microsoft® Visual C, **_beginthread ®** , **_endthread** (o **_beginthreadex** e **_endthreadex**) per creare e terminare thread che chiamano Gestione driver ODBC. Se invece le applicazioni chiamano le funzioni **CreateThread** ed **EndThread** di Microsoft Windows NT®, si verificheranno perdite di memoria perché Gestione Driver e alcuni driver ODBC chiamano funzioni di runtime C che non funzioneranno su un thread creato chiamando **CreateThread**. Per altre informazioni, vedere la documentazione di Microsoft Windows®.
