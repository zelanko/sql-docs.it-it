---
title: Introduzione a SQL Server (on Linux) nel Cloud
titleSuffix: SQL Server
description: Questa Guida introduttiva illustra come eseguire SQL Server in Linux nel cloud di propria scelta.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 3c64c2ab3927c111b29f0bafa6745fbab2f7fd13
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160539"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>Guida introduttiva: Eseguire SQL Server nel cloud

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In questa Guida introduttiva si installerà SQL Server su Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) o Ubuntu nel cloud di propria scelta. Passare a [effettuare il provisioning di una macchina virtuale Linux di SQL Server nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) per eseguire SQL Server su Linux in Azure.

> [!NOTE]
> Se si sceglie di eseguire un'edizione a pagamento di SQL Server, quindi è necessario utilizzare la propria licenza (BYOL).

## <a name="amazon-web-services"></a>Servizi Web Amazon
1.  Creare un AMI Linux con almeno 2 GB di memoria da marketplace 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES 12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Connettersi alla finestra di Rispostarli con ssh
1.  Attenersi alla Guida introduttiva per la distribuzione Linux che scelta: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurare connessioni remote: 
    * Aprire il [console di Amazon EC2]( https://console.aws.amazon.com/ec2/)
    * Nel riquadro di spostamento, scegliere **gruppi di sicurezza**. 
    * Scegliere **in ingresso, modifica, aggiungere una regola**
    * Aggiungere una regola in ingresso per consentire il traffico sulla porta su cui SQL Server è in ascolto (porta TCP predefinita 1433)

    
## <a name="digital-ocean"></a>Digital Ocean
1. Accedi per il [Pannello di controllo](https://cloud.digitalocean.com/login) e fare clic su Crea un droplet
1. Scegliere un droplet Ubuntu 16.04 con almeno 2 GB di memoria
1. Connettersi al droplet con ssh
1. Seguire il [avvio rapido di Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configurare connessioni remote:
    * Nella parte superiore del Pannello di controllo, seguire le **Networking** collegamento e quindi selezionare **firewall**
    * Aggiungere una regola in ingresso per consentire il traffico sulla porta su cui SQL Server è in ascolto (porta TCP predefinita 1433)
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  Creare un'immagine Linux con almeno 2 GB di memoria di avvio di Cloud 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES 12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Connettersi all'immagine con ssh
1.  Attenersi alla Guida introduttiva per la distribuzione Linux che scelta: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurare connessioni remote: 
    * Andare alla [regole del Firewall](https://console.cloud.google.com/networking/firewalls)
    * Aggiungere una regola in ingresso per consentire il traffico sulla porta su cui è in ascolto SQL Server (default tcp: 1433)
