---
title: Impostazione delle proprietà dell'origine dati
description: Informazioni sulle origini dati in JDBC e su come impostare le relative proprietà per configurare l'accesso al database con Java.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a2a9964b592fc1bcb8c41cf0c5b8de67a2d5a18
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411337"
---
# <a name="setting-the-data-source-properties"></a>Impostazione delle proprietà dell'origine dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Le origini dati sono il meccanismo ideale con cui creare connessioni JDBC in un ambiente Java EE (Java Platform, Enterprise Edition). Le origini dati forniscono connessioni, connessioni in pool e connessioni distribuite senza la necessità di specificare le proprietà di connessione a livello di codice Java. Tutte le origini dati di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] consentono di impostare o ottenere il valore di qualsiasi proprietà usando rispettivamente i metodi setter e getter appropriati.

I prodotti Java EE, quali server applicazioni e motori servlet/JSP, consentono in genere di configurare origini dati per l'accesso ai database. Tutte le proprietà elencate nell'argomento [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md) possono essere specificate ovunque la configurazione consenta di immettere una proprietà come coppia proprietà=valore.

Per altre informazioni sulle origini dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). Per un esempio di come usare la classe SQLServerDataSource per creare una connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Esempio di origine dati](../../connect/jdbc/data-source-sample.md).

## <a name="see-also"></a>Vedere anche

[Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
