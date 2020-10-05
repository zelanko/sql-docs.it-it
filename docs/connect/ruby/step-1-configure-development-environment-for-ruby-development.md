---
title: "Passaggio 1: Configurare l'ambiente di sviluppo per Ruby"
description: Il passaggio 1 di questa guida introduttiva prevede l'installazione di Ruby e di un driver ODBC per SQL Server nell'ambiente di sviluppo.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6412015000a5f9dda09ea5d489c8080fd2e1c09
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603367"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Ruby
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver Ruby per SQL Server.    
  
Il driver Ruby usa il protocollo TDS che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Scaricare il programma di installazione di Ruby**  
Se nel computer non è installato Ruby, installarlo. Per i nuovi utenti Ruby, è consigliabile usare i programmi di installazione Ruby 2.2.X, che offrono un linguaggio stabile e un elenco completo di pacchetti (gem) compatibili e aggiornati. Passare alla [pagina di download di Ruby](https://rubyinstaller.org/downloads/) e scaricare il programma di installazione 2.1.x appropriato. Se ad esempio si usa un computer a 64 bit, scaricare il programma di installazione di Ruby 2.1.6 (x64).   
  
2.  **Installare Ruby**  
Dopo aver scaricato il programma di installazione:  
a. Fare doppio clic sul file per avviare il programma di installazione.  
b. Selezionare la lingua e accettare le condizioni.  
c.  Nella schermata delle impostazioni di installazione selezionare le caselle di controllo accanto ad Add Ruby executables to your PATH (Aggiungi gli eseguibili Ruby a PATH) e Associate `.rb` and `.rbw` files with this Ruby installation (Associa i file con estensione rb e rbw a questa installazione di Ruby).  
  
3.  **Scaricare il kit di sviluppo di Ruby**  
Scaricare il kit di sviluppo dalla pagina del programma di installazione di Ruby  
  
4.  **Installare il kit di sviluppo di Ruby**  
Al termine del download:  
a. Fare doppio clic sul file. Verrà richiesto di specificare la posizione in cui estrarre i file.  
b. Fare clic sul pulsante "..." e selezionare "C:\DevKit". È probabile che sia necessario creare prima questa cartella facendo clic su "Crea nuova cartella".  
c. Fare clic su "OK" e quindi su "Extract" (Estrai) per estrarre i file.  
  
5. **Aprire cmd.exe**  
  
6. **Inizializzare il kit di sviluppo di Ruby**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Installare la gemma TinyTDS**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Aprire il terminale**  
  
2. **Installare Ruby Version Manager (`rvm`) e i prerequisiti**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Usare `rvm` per installare Ruby**  
Ad esempio, installare la versione 2.3.0 di Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Verificare che l'output dell'ultimo comando indichi che si sta eseguendo la versione 2.3.0.  
  
4.  **Installare FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Installare TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="macos"></a>macOS  
  
Nota: in macOS è già preinstallato Ruby poiché il sistema operativo ha una dipendenza.
  
1.  **Aprire il terminale**  
  
2. **Installare la gestione pacchetti Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Installare FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Installare la gemma TinyTDS**  
```  
> gem install tiny_tds  
```
