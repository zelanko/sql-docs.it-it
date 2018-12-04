---
title: Distribuzione del Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c677cd46b4d3366b997e4d1effe5c056ec62a158
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529601"
---
# <a name="deploying-the-jdbc-driver"></a>Distribuzione del driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si distribuisce un'applicazione che dipende da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], è necessario ridistribuire il driver JDBC insieme all'applicazione. Diversamente da Windows Data Access Components (Windows DAC), che è un componente del sistema operativo Windows, il driver JDBC è considerato un componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esistono due approcci per la distribuzione del driver JDBC con l'applicazione. Un approccio prevede l'inclusione dei file del driver JDBC come parte del pacchetto di installazione personalizzato. Il secondo approccio prevede l'usp del pacchetto di installazione JDBC fornito da Microsoft, scaricabile in [Microsoft JDBC Driver per SQL Server](https://go.microsoft.com/fwlink/?LinkId=70166).  
  
 Nelle sezioni seguenti viene descritto come utilizzare il pacchetto di installazione JDBC in sistemi operativi Windows e UNIX.  
  
> [!NOTE]  
>  Per informazioni generali sulla distribuzione di applicazioni Java, vedere il sito Web Java.  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Distribuzione del driver JDBC in sistemi Windows  
 Per distribuire il driver JDBC in sistemi operativi Windows, è necessario usare la versione del file ZIP eseguibile del pacchetto di installazione, denominata in genere `sqljdbc_<version>_<language>.exe`.  
  
 Per l'esecuzione automatica del file eseguibile ZIP, è necessario usare l'opzione della riga di comando `/auto` nella riga di comando o in un file batch nel modo seguente:  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  Quando si usa l'opzione `/auto` l'installazione non sarà realmente automatica, in quanto la finestra di dialogo di WinZip verrà comunque visualizzata sullo schermo dell'utente. Tuttavia, non è necessario interagire con essa e viene chiusa non appena l'operazione di decompressione è stata completata.  
  
## <a name="deploying-the-driver-on-unix-systems"></a>Distribuzione del driver su sistemi UNIX  
 Quando il driver JDBC viene distribuito in sistemi operativi UNIX, è necessario utilizzare la versione del file GZIP del pacchetto di installazione, denominata in genere `sqljdbc_<version>_<language>.tar.gz`.  
  
 Prima di installare il driver JDBC, assicurarsi che entrambe le utilità GZIP e TAR siano installate nel sistema operativo dell'utente e che le cartelle che contengono i file eseguibili di entrambe le utilità siano state aggiunte alla variabile di ambiente PATH.  
  
 Per decomprimere il file con estensione tar compresso, passare alla directory in cui si desidera decomprimere il driver e digitare il comando seguente:  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 Per decomprimere il file con estensione tar, spostarlo nella directory in cui si desidera installare il driver e digitare il comando seguente:  
  
 `tar -xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
