---
title: Znane problemy i rozwiązywanie problemów
titleSuffix: Azure Machine Learning service
description: Pobierz listę znanych problemów, obejścia problemu i rozwiązywanie problemów dotyczących usługi Azure Machine Learning.
services: machine-learning
author: j-martens
ms.author: jmartens
ms.reviewer: mldocs
ms.service: machine-learning
ms.subservice: core
ms.topic: article
ms.date: 12/04/2018
ms.custom: seodec18
ms.openlocfilehash: b10e434aece0ac214a0fd397ea94cbeccca4e44a
ms.sourcegitcommit: 947b331c4d03f79adcb45f74d275ac160c4a2e83
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/05/2019
ms.locfileid: "55746494"
---
# <a name="known-issues-and-troubleshooting-azure-machine-learning-service"></a>Znane problemy i rozwiązywania problemów z usługi Azure Machine Learning

Ten artykuł ułatwia znajdowanie i poprawić błędy lub błędów napotkanych podczas korzystania z usługi Azure Machine Learning.

## <a name="sdk-installation-issues"></a>Problemy z instalacją zestawu SDK

**Komunikat o błędzie: Nie można odinstalować "PyYAML"**

Środowisko Azure Machine Learning zestawu SDK dla języka Python: PyYAML jest projektem zainstalowanych distutils. W związku z tym firma Microsoft nie można dokładnie określić pliki, które należą do niej w przypadku częściowej dezinstalacji. Aby kontynuować instalację zestawu SDK podczas ignorowanie tego błędu, należy użyć:

```Python
pip install --upgrade azureml-sdk[notebooks,automl] --ignore-installed PyYAML
```

## <a name="trouble-creating-azure-machine-learning-compute"></a>Problemy z utworzeniem obliczeniowego usługi Azure Machine Learning

Brak rzadkich prawdopodobieństwo, że niektórych użytkowników, którzy utworzyli swój obszar roboczy usługi Azure Machine Learning w witrynie Azure portal przed wydaniem Ogólnodostępnej mogą nie można utworzyć obliczeniowego usługi Azure Machine Learning, w tym obszarze roboczym. Możesz zgłosić żądanie pomocy technicznej, korzystająca z usługi lub Utwórz nowy obszar roboczy za pośrednictwem portalu lub zestawu SDK, aby odblokować samodzielnie natychmiast.

## <a name="image-building-failure"></a>Błąd tworzenia obrazu

Obraz tworzenia niepowodzenia podczas wdrażania usługi sieci web. Obejście polega na dodawanie "pynacl == 1.2.1" jako zależność pip Conda pliku konfiguracji obrazu.

## <a name="deployment-failure"></a>Wdrożenie zakończyło się niepowodzeniem

Jeśli zauważysz `['DaskOnBatch:context_managers.DaskOnBatch', 'setup.py']' died with <Signals.SIGKILL: 9>`, zmiana jednostki SKU dla maszyn wirtualnych używanych we wdrożeniu na taki, który ma więcej pamięci.

## <a name="fpgas"></a>Układy FPGA
Nie można wdrażać modele na układów FPGA dopiero po przeprowadzeniu mają wymagane i zostało zatwierdzone dla limitu przydziału FPGA. Aby zażądać dostępu, wypełnij formularz żądania limitu przydziału: https://aka.ms/aml-real-time-ai

## <a name="databricks"></a>Databricks

Problemy z usługi Databricks i Azure Machine Learning.

1. Błędy instalacji usługi Azure Machine Learning w zestawie SDK w usłudze Databricks, podczas instalowania dodatkowych pakietów.

   Niektóre pakiety, takich jak `psutil`, mogą powodować konflikty. Aby uniknąć błędów instalacji, należy zainstalować pakiety zamrożenia wersji lib. Ten problem jest związany z Databricks i Azure Machine Learning Usługa SDK — użytkownik może prawdzie z innymi bibliotekami zbyt. Przykład:
   ```python
   pstuil cryptography==1.5 pyopenssl==16.0.0 ipython==2.2.0
   ```
   Alternatywnie można użyć skryptów init, jeśli możesz zachować problemów z instalacją przy użyciu bibliotek języka Python. To podejście nie jest oficjalnie obsługiwanych podejście. Możesz zapoznać się z [tego dokumentu](https://docs.azuredatabricks.net/user-guide/clusters/init-scripts.html#cluster-scoped-init-scripts).

2. Korzystając z automatycznych uczenia maszynowego w usłudze Databricks, jeśli chcesz anulować przebieg i uruchom nowy eksperyment Uruchom, uruchom ponownie usługi Azure Databricks w klastrze.

3. W ustawieniach ml automatyczne, jeśli masz więcej niż 10 iteracji, ustaw `show_output` do `False` momentu przesłania przebiegu.


## <a name="azure-portal"></a>Azure Portal
Jeśli przejdziesz bezpośrednio, aby wyświetlić obszar roboczy z Udostępnij link z zestawu SDK lub w portalu, nie można wyświetlić strony z normalnej Przegląd informacji o subskrypcji w rozszerzeniu. Ponadto nie można przełączyć się do innego obszaru roboczego. Jeśli potrzebujesz wyświetlić inny obszar roboczy, obejście polega na przejść bezpośrednio do [witryny Azure portal](https://portal.azure.com) i wyszukaj nazwę obszaru roboczego.

## <a name="diagnostic-logs"></a>Dzienniki diagnostyczne
Czasami może być przydatne Jeśli podasz informacje diagnostyczne podczas pytania o pomoc.
Oto, miejsca zamieszkania pliki dziennika:

## <a name="resource-quotas"></a>Limity przydziałów zasobów

Dowiedz się więcej o [limity przydziałów zasobów](how-to-manage-quotas.md) można napotkać podczas pracy z usługą Azure Machine Learning.

## <a name="authentication-errors"></a>Błędy uwierzytelniania

Jeśli operacja zarządzania w celu obliczeń z zadania zdalne, zostanie wyświetlony jeden z następujących błędów:

```json
{"code":"Unauthorized","statusCode":401,"message":"Unauthorized","details":[{"code":"InvalidOrExpiredToken","message":"The request token was either invalid or expired. Please try again with a valid token."}]}
```

```json
{"error":{"code":"AuthenticationFailed","message":"Authentication failed."}}
```

Na przykład zostanie wyświetlony błąd, jeśli zostanie podjęta próba Utwórz lub Dołącz obliczeniowego elementu docelowego z potoku uczenia Maszynowego, który jest przesyłany w celu wykonania zdalnego.

## <a name="get-more-support"></a>Uzyskaj więcej obsługę

Możesz przesyłać żądania pomocy technicznej i poproś pomoc techniczną, fora i inne. [Dowiedz się więcej...](support-for-aml-services.md)
