---
title: Stosowanie aktualizacji w usłudze Azure Stack | Dokumentacja firmy Microsoft
description: Dowiedz się, jak importować i instalowania pakietów aktualizacji programu Microsoft system zintegrowany z usługi Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/11/2019
ms.author: mabrigg
ms.reviewer: justini
ms.lastreviewed: 02/11/2019
ms.openlocfilehash: 0c3f52c78bbfd3094324b74f3b66610fcebfa2f4
ms.sourcegitcommit: 39397603c8534d3d0623ae4efbeca153df8ed791
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56099296"
---
# <a name="apply-updates-in-azure-stack"></a>Stosowanie aktualizacji w usłudze Azure Stack

*Dotyczy: Zintegrowane systemy usługi Azure Stack*

Możesz użyć **aktualizacji** kafelka w portalu administracyjnym, aby zastosować pakietów aktualizacji firmy Microsoft lub producentem OEM dla usługi Azure Stack.

Jeśli używasz wersji systemów zintegrowanych 1807 lub wcześniej, należy pobrać pakiet aktualizacji, importowania plików pakietu do usługi Azure Stack, a następnie zainstaluj pakiet aktualizacji. Aby uzyskać instrukcje, zobacz [aktualizacji usługi Azure Stack przez pobieranie pakietu](#update-azure-stack-by-downloading-the-package)

Uaktualnij te instrukcje pracy przy użyciu usługi Azure Stack, zintegrowanych systemów. Jeśli używasz systemu Azure dla deweloperów stosu należy pobrać pakiet instalacyjny dla bieżącej wersji. Aby uzyskać instrukcje, zobacz [Zainstaluj zestaw Azure Stack Development Kit](.\asdk\asdk-install.md)

## <a name="update-azure-stack"></a>Aktualizacja usługi Azure Stack

### <a name="select-and-apply-an-update-package"></a>Wybierz i zastosuj pakiet aktualizacji

1. Otwórz w portalu administratora.

2. Wybierz **pulpit nawigacyjny**. Wybierz **aktualizacji** kafelka.

    ![Dostępna aktualizacja usługi Azure Stack](media/azure-stack-apply-updates/azure-stack-updates-1901-dashboard.png)

3. Zanotuj bieżącą wersję usługi Azure Stack. Możesz zaktualizować do następnej pełnej wersji. Na przykład jeśli korzystasz usługi Azure Stack 1811 następnego udostępniono wersję jest 1901.

    ![Zastosuj aktualizacja usługi Azure Stack](media/azure-stack-apply-updates/azure-stack-updates-1901-updateavailable.png)

4. Zaznacz następną dostępną wersję na liście aktualizacji. Możesz wybrać **widoku** w wersji informacje o kolumnie, aby otworzyć temacie Informacje o wersji dla wersji, jeśli chcesz przejrzeć zmiany wersji.

5. Wybierz opcję aktualizacji. Aktualizacja rozpocznie się.

### <a name="review-update-history"></a>Przejrzyj historię aktualizacji

1. Otwórz w portalu administratora.

2. Wybierz **pulpit nawigacyjny**. Wybierz **aktualizacji** kafelka.

3. Wybierz **aktualizacji historii**.

![Historię aktualizacji w usłudze Azure Stack](media/azure-stack-apply-updates/azure-stack-update-history.PNG)

## <a name="update-azure-stack-by-downloading-the-package"></a>Aktualizacja usługi Azure Stack przez pobieranie pakietu

Jeśli używasz wersji systemów zintegrowanych 1807 lub wcześniej, należy pobrać pakiet aktualizacji, importowania plików pakietu do usługi Azure Stack, a następnie zainstaluj pakiet aktualizacji.

## <a name="download-the-update-package"></a>Pobierz pakiet aktualizacji

Gdy dostępny jest pakiet aktualizacji firmy Microsoft lub producentem OEM dla usługi Azure Stack, Pobierz pakiet w lokalizacji, który jest dostępny z poziomu usługi Azure Stack, a następnie przejrzyj zawartość pakietu. Pakiet aktualizacji na ogół składa się z następujących plików:

- Samowyodrębniający `<PackageName>.exe` pliku. Ten plik zawiera ładunek do aktualizacji, na przykład najnowszej aktualizacji zbiorczej dla systemu Windows Server.

- Odpowiadające `<PackageName>.bin` plików. Pliki te zapewniają kompresja ładunek, który jest skojarzony z *Nazwa_pakietu*pliku .exe.

- A `Metadata.xml` pliku. Ten plik zawiera podstawowe informacje dotyczące aktualizacji, na przykład wydawcy, nazwa, wstępnie wymaganego składnika, rozmiar i adres URL pomocy technicznej ścieżki.

> [!IMPORTANT]  
> Po zastosowaniu pakietu aktualizacji usługi Azure Stack 1901 format pakowania pacakges aktualizacji usługi Azure Stack zostaną przeniesione z .exe, .bin(s) i format XML .zip(s) i format XML. Operatorzy usługi Azure Stack, które połączyły sygnatury nie będą mieć wpływ. Operatorzy usługi Azure Stack, które zostały odłączone po prostu zostaną zaimportowane pliki XML i zip przy użyciu tego samego procesu opisanego poniżej.

## <a name="import-and-install-updates"></a>Importowanie i zainstaluj aktualizacje

Poniższa procedura pokazuje, jak zaimportować, a następnie zainstaluj pakiety aktualizacji w portalu administratora.

> [!IMPORTANT]  
> Zdecydowanie zalecamy powiadomienie użytkowników dowolne operacje konserwacji i planowania konserwacji systemu windows podczas poza godzinami możliwie. Operacje konserwacji może mieć wpływ na użytkownika obciążeń i operacje w portalu.

1. W portalu administratora wybierz **wszystkich usług**. Następnie w obszarze **dane + magazyn** kategorii, wybierz opcję **kont magazynu**. (Lub w polu filtru zacznij wpisywać ciąg **kont magazynu**, a następnie wybierz ją.)

    ![Pokazuje, gdzie można znaleźć konta magazynu w portalu](media/azure-stack-apply-updates/ApplyUpdates1.png)

2. W polu filtru wpisz **aktualizacji**i wybierz **updateadminaccount** konta magazynu.

3. W magazynie ekranu szczegóły konta, w obszarze **usług**, wybierz opcję **obiektów blob**.
 
    ![Pokazuje, jak uzyskać dostęp do obiektów blob dla konta magazynu](media/azure-stack-apply-updates/ApplyUpdates3.png) 

4. W obszarze **usługi Blob service**, wybierz opcję **+ kontener** do utworzenia kontenera. Wprowadź nazwę (na przykład *1811 aktualizacji*), a następnie wybierz pozycję **OK**.
 
     ![Pokazuje, jak dodać kontener na koncie magazynu](media/azure-stack-apply-updates/ApplyUpdates4.png)

5. Po utworzeniu kontenera, kliknij nazwę kontenera, a następnie kliknij przycisk **przekazywanie** przekazywania plików pakietu do kontenera.
 
    ![Pokazuje sposób przekazywania plików pakietu](media/azure-stack-apply-updates/ApplyUpdates5.png)

6. W obszarze **przekazywanie obiektu blob**, kliknij ikonę folderu, wskaż lokalizację pakietu aktualizacji plik .exe, a następnie kliknij przycisk **Otwórz** w oknie Eksploratora plików.
  
7. W obszarze **przekazywanie obiektu blob**, kliknij przycisk **przekazywanie**.
  
    ![Wskazuje, gdzie w celu przekazania wszystkich plików pakietu](media/azure-stack-apply-updates/ApplyUpdates6.png)

8. Powtórz kroki 6 i 7 dla *Nazwa_pakietu*bin i pliki Metadata.xml. Nie należy importować plik uzupełniające plik Notice.txt, jeśli uwzględniony.
9. Gdy skończysz, możesz przejrzeć powiadomienia (ikonę dzwonka w prawym górnym rogu portalu). Powiadomienia powinny wskazywać, że przekazywanie ukończone.
10. Przejdź z powrotem do Aktualizuj Kafelek na pulpicie nawigacyjnym. Kafelek powinno wskazywać, że dostępna jest aktualizacja. Kliknij Kafelek, aby przejrzeć pakiet aktualizacji nowo dodane.
11. Aby zainstalować aktualizację, wybierz pakiet, który jest oznaczony jako **gotowe** a albo kliknij prawym przyciskiem myszy pakiet i wybierz **teraz zaktualizować**, lub kliknij przycisk **teraz zaktualizować** akcji w prawym górnym .
12. Po kliknięciu instalowania pakietu aktualizacji, można wyświetlić stan w **szczegóły przebiegu aktualizacji** obszaru. W tym miejscu możesz również kliknąć **Pobierz pełne dzienniki** do pobierania plików dziennika.
13. Po zakończeniu aktualizacji, Aktualizuj Kafelek zawiera zaktualizowaną wersję usługi Azure Stack.

Można ręcznie usunąć aktualizacje z konta magazynu, po ich zainstalowaniu w usłudze Azure Stack. Usługa Azure Stack okresowo sprawdza dostępność starszych pakietów aktualizacji i usuwa je z magazynu. Może upłynąć usługi Azure Stack dwa tygodnie, aby usunąć stare pakiety.

## <a name="next-steps"></a>Kolejne kroki

- [Zarządzanie aktualizacjami w usłudze Azure Stack — omówienie](azure-stack-updates.md)
- [Obsługa zasad z usługi Azure Stack](azure-stack-servicing-policy.md)
