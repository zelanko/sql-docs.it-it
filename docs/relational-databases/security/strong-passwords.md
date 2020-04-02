---
title: Password complesse | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 297dc4127fbfd040ba0d9cc970f3a044395b5e21
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79448228"
---
# <a name="strong-passwords"></a>Password complesse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Le password possono costituire il punto debole nell'ambito distribuzione della sicurezza in un server. Prestare grande attenzione alla scelta delle password. Una password complessa ha le caratteristiche seguenti:  
  
-   Contiene almeno otto caratteri.  
  
-   È costituita da una combinazione di lettere, numeri e simboli.  
  
-   Non è una parola presente nei dizionari.  
  
-   Non è il nome di un comando.  
  
-   Non è il nome di una persona.  
  
-   Non è il nome di un utente.  
  
-   Non è il nome di un computer.  
  
-   Viene modificata regolarmente.  
  
-   Presenta differenze rispetto alle password precedenti.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le password possono contenere fino a 128 caratteri, compresi lettere, simboli e cifre. Poiché gli account di accesso, i nomi utente, i ruoli e le password vengono spesso utilizzati in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , è necessario racchiudere alcuni simboli tra virgolette doppie (") o parentesi quadre ([ ]). Utilizzare questi delimitatori nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] quando l'account di accesso, l'utente, il ruolo o la password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenta le caratteristiche seguenti:  
  
-   Include o inizia con uno spazio.  
  
-   Inizia con il carattere $ o \@.  
  
 Gli account di accesso e le password usati in una stringa di connessione OLE DB o ODBC non devono contenere i caratteri seguenti: [] () , ; ? * ! \@ =. Questi caratteri vengono utilizzati per inizializzare una connessione o per separare i relativi valori.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Criteri password](../../relational-databases/security/password-policy.md)  
  
  
