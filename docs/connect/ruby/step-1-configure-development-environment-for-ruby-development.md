---
title: "Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Ruby | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992467"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Ruby
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione mediante il driver Ruby per SQL Server.    
  
Si noti che il driver Ruby usa il protocollo TDS, che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Scarica programma di installazione Ruby**  
Se il computer non dispone di Ruby, installarlo. Per i nuovi utenti Ruby, è consigliabile usare i programmi di installazione Ruby 2.2. X. Questi forniscono un linguaggio stabile e un ampio elenco di pacchetti (gemme) compatibili e aggiornati. Passare alla [pagina di download di Ruby](https://rubyinstaller.org/downloads/) e scaricare il programma di installazione 2.1. x appropriato. Ad esempio, se si è in un computer a 64 bit, scaricare il programma di installazione Ruby 2.1.6 (x64).   
  
2.  **Installare Ruby**  
Una volta scaricato il programma di installazione, eseguire le operazioni seguenti:  
A. Fare doppio clic sul file per avviare il programma di installazione.  
B. Selezionare la lingua e accettare le condizioni.  
c.  Nella schermata Installa impostazioni selezionare le caselle di controllo accanto a Aggiungi eseguibili Ruby al percorso e associare i file con estensione RB e RBW a questa installazione di Ruby.  
  
3.  **Scarica Ruby DevKit**  
Scaricare DevKit dalla pagina RubyInstaller  
  
4.  **Installare Ruby DevKit**  
Al termine del download, eseguire le operazioni seguenti:  
A. Fare doppio clic sul file. Verrà richiesto dove estrarre i file.  
B. Fare clic su "..." e selezionare "C:\DevKit". Probabilmente sarà necessario creare prima questa cartella facendo clic su "Crea nuova cartella".  
c. Fare clic su "OK" e quindi su "Estrai" per estrarre i file.  
  
5. **Apri cmd. exe**  
  
6. **Inizializzare Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Installare funzione tinytds Gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Apri terminale**  
  
2. **Installare Ruby Version Manager (RVM) e i prerequisiti**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Usare RVM per installare Ruby**  
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
  
5.  **Installare funzione tinytds**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Si noti che Mac OS X dispone già di Ruby pre-installato, perché il sistema operativo ha una dipendenza.    
  
1.  **Apri terminale**  
  
2. **Installare Homebrew Package Manager**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Installare FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Installare funzione tinytds Gem**  
```  
> gem install tiny_tds  
```
