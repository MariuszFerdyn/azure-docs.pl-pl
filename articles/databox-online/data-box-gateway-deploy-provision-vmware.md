---
title: Samouczek dotyczący aprowizacji usługi Azure Data Box Gateway w programie VMware | Microsoft Docs
description: W drugim samouczku dotyczącym wdrażania usługi Azure Data Box Gateway omówiono aprowizację urządzenia wirtualnego w programie VMware.
services: databox
author: alkohli
ms.service: databox
ms.subservice: gateway
ms.topic: tutorial
ms.date: 01/28/2019
ms.author: alkohli
ms.openlocfilehash: 00415cab4d5c36c74cf78a10cb71682d97236517
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2019
ms.locfileid: "55099162"
---
# <a name="tutorial-provision-azure-data-box-gateway-in-vmware-preview"></a>Samouczek: aprowizowanie usługi Azure Data Box Gateway w programie VMware (wersja zapoznawcza)

## <a name="overview"></a>Omówienie

W tym samouczku opisano sposób aprowizacji usługi Data Box Gateway w systemie hosta, w którym działa program VMware ESXi 6.0, 6.5 lub 6.7. 

Do aprowizowania urządzenia wirtualnego i nawiązania z nim połączenia wymagane są uprawnienia administratora. Aprowizacja i wstępna konfiguracja może zająć około 10 minut.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Sprawdzanie, czy host spełnia minimalne wymagania dotyczące urządzenia
> * Aprowizowanie urządzenia wirtualnego w programie VMware
> * Uruchamianie urządzenia wirtualnego i uzyskiwanie adresu IP

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

> [!IMPORTANT]
> - Usługa Data Box Gateway jest dostępna w wersji zapoznawczej. Przed zamówieniem i wdrożeniem tego rozwiązania zapoznaj się z [warunkami świadczenia usług Azure w wersji zapoznawczej](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="prerequisites"></a>Wymagania wstępne

Wymagania wstępne, które muszą być spełnione, aby można było aprowizować urządzenie wirtualne na systemie hosta z programem VMware ESXi 6.0, 6.5 lub 6.7 są następujące.

### <a name="for-the-data-box-gateway-resource"></a>Zasób usługi Data Box Gateway

Przed rozpoczęciem upewnij się, że:

* Zostały wykonane wszystkie kroki samouczka [Prepare the portal for Data Box Gateway (Przygotowywanie portalu pod kątem usługi Data Box Gateway)](data-box-gateway-deploy-prep.md).
* Pobrano obraz urządzenia wirtualnego dla programu VMware z witryny Azure Portal zgodnie z opisem w samouczku [Prepare the portal for Data Box Gateway (Przygotowywanie portalu pod kątem usługi Data Box Gateway)](data-box-gateway-deploy-prep.md).

  > [!IMPORTANT]
  > Oprogramowania uruchomionego w usłudze Data Box Gateway można używać tylko z zasobem usługi Data Box Gateway.

### <a name="for-the-data-box-gateway-virtual-device"></a>Urządzenie wirtualne usługi Data Box Gateway

Przed wdrożeniem urządzenia wirtualnego upewnij się, że są spełnione następujące warunki:

* Masz dostęp do systemu hosta z programem VMware (ESXi 6.0, 6.5 lub 6.7), którego można użyć do aprowizacji urządzenia.
* System hosta może przeznaczyć następujące zasoby wyłącznie na potrzeby aprowizacji urządzenia wirtualnego:

  * Co najmniej 4 rdzenie.
  * Co najmniej 8 GB pamięci RAM.
  * Jeden interfejs sieciowy.
  * Dysk systemu operacyjnego o rozmiarze 250 GB.
  * Dysk wirtualny o rozmiarze 2 TB do przechowywania danych systemu.

### <a name="for-the-network-in-datacenter"></a>Sieć w centrum danych

Przed rozpoczęciem:

- Zapoznaj się z wymaganiami dotyczącymi przygotowania sieci pod kątem wdrożenia usługi Data Box Gateway i skonfiguruj sieć w centrum danych zgodnie z tymi wymaganiami. Aby uzyskać więcej informacji, zobacz [Data Box Gateway networking requirements (Wymagania dotyczące sieci dla usługi Data Box Gateway)](data-box-gateway-system-requirements.md#networking-requirements).
- Aby umożliwić optymalne działanie urządzenia, przepustowość połączenia internetowego musi wynosić co najmniej 20 Mb/s.

## <a name="check-the-host-system"></a>Sprawdzanie systemu hosta

Do utworzenia urządzenia wirtualnego potrzebne są następujące elementy:

* Dostęp do systemu hosta z programem VMware ESXi Server 6.0, 6.5 lub 6.7. System hosta może przeznaczyć następujące zasoby wyłącznie na potrzeby urządzenia wirtualnego:
 
  * Co najmniej 4 rdzenie.
  * Co najmniej 8 GB pamięci RAM. 
  * Jeden interfejs sieciowy połączony z siecią umożliwiającą kierowanie ruchu do Internetu. 
  * Dysk systemu operacyjnego o rozmiarze 250 GB.
  * Dysk wirtualny o rozmiarze 2 TB do przechowywania danych.
* Klient VMware vSphere w systemie na potrzeby zarządzania hostem ESXi.


## <a name="provision-a-virtual-device-in-hypervisor"></a>Aprowizowanie urządzenia wirtualnego w funkcji hypervisor

Wykonaj następujące czynności, aby aprowizować urządzenie wirtualne w funkcji hypervisor.

1. Skopiuj obraz urządzenia wirtualnego do swojego systemu. Ten obraz urządzenia wirtualnego (dwa pliki) został pobrany za pośrednictwem witryny Azure Portal. Zanotuj lokalizację, do której został skopiowany obraz, ponieważ będzie on używany w dalszej części tej procedury.

2. Zaloguj się na serwerze ESXi przy użyciu klienta internetowego vSphere. Musisz mieć uprawnienia administratora, aby utworzyć maszynę wirtualną.

   ![](./media/data-box-gateway-deploy-provision-vmware/image1.png)
  
3. Przekaż dysk VMDK na serwer ESXi. W okienku Navigator (Nawigator) wybierz pozycję **Storage** (Magazyn).

   ![](./media/data-box-gateway-deploy-provision-vmware/image2.png)

4. W okienku po prawej stronie, w obszarze **Datastores** (Magazyny danych), wybierz magazyn danych, do którego chcesz przekazać dysk VMDK. 

    - Magazyn danych musi być typu VMFS5. 
    - Magazyn danych musi również mieć wystarczającą ilość wolnego miejsca dla dysków systemu operacyjnego i danych.
   
5. Kliknij prawym przyciskiem myszy i wybierz polecenie **Browse Datastore** (Przeglądaj magazyn danych).

   ![](./media/data-box-gateway-deploy-provision-vmware/image3.png)

6. Zostanie wyświetlone okno **Datastore Browser** (Przeglądarka magazynu danych).

   ![](./media/data-box-gateway-deploy-provision-vmware/image4.png)

7. Na pasku narzędzi kliknij ikonę **Create directory** (Utwórz katalog), aby utworzyć nowy folder. Określ nazwę folderu i zanotuj ją. Ta nazwa folderu będzie używana później, podczas tworzenia maszyny wirtualnej (zalecane najlepsze rozwiązanie). Kliknij pozycję **Create directory** (Utwórz katalog).

   ![](./media/data-box-gateway-deploy-provision-vmware/image5.png)

8. Nowy folder zostanie wyświetlony w okienku po lewej stronie okna **Datastore Browser** (Przeglądarka magazynu danych). Kliknij ikonę **Upload** (Przekaż), a następnie wybierz pozycję **Upload File** (Przekaż plik).

    ![](./media/data-box-gateway-deploy-provision-vmware/image6.png)

9. Wskaż pobrane pliki VMDK. Pliki są dwa. Wybierz plik do przekazania.

    ![](./media/data-box-gateway-deploy-provision-vmware/image7.png)

10. Kliknij przycisk **Open** (Otwórz). Rozpocznie się przekazywanie pliku VMDK do określonego magazynu danych. Przekazanie pliku może zająć kilka minut.
11. Po zakończeniu przekazywania plik będzie widoczny w magazynie danych w utworzonym folderze. Teraz przekaż drugi plik VMDK do tego samego magazynu danych. Po przekazaniu obu plików zostaną one scalone w jeden plik. Wtedy w katalogu będzie widoczny pojedynczy plik.

    ![](./media/data-box-gateway-deploy-provision-vmware/image8.png)

12. Wróć do okna klienta vSphere. W okienku Navigator (Nawigator) wybierz pozycję **Virtual Machines** (Maszyny wirtualne). W okienku po prawej stronie kliknij pozycję **Create/Register VM** (Utwórz/zarejestruj maszynę wirtualną).

    ![](./media/data-box-gateway-deploy-provision-vmware/image9.png)

13. Zostanie wyświetlone okno **New Virtual Machine** (Nowa maszyna wirtualna). W obszarze Select creation type (Wybór typu tworzenia) wybierz pozycję **Create a new virtual machine** (Utwórz nową maszynę wirtualną) i kliknij przycisk **Next** (Dalej).
    ![](./media/data-box-gateway-deploy-provision-vmware/image10.png)

14. Na stronie **Select a Name and OS Name and Location** (Wybór nazwy, nazwy systemu operacyjnego i lokalizacji) określ nazwę maszyny wirtualnej w polu **Name** (Nazwa). Ta nazwa powinna odpowiadać nazwie folderu (zalecane najlepsze rozwiązanie), którą podano wcześniej w kroku 7. W polu **Guest OS family** (Rodzina systemu operacyjnego gościa) wybierz pozycję Windows, a w polu **Guest OS version** (Wersja systemu operacyjnego gościa) — Microsoft Windows Server 2016 (64-bit) (Microsoft Windows Server 2016 [64-bitowy]). Kliknij przycisk **Dalej**.

    ![](./media/data-box-gateway-deploy-provision-vmware/image11.png)

15. Na stronie **Select storage** (Wybór magazynu) wybierz magazyn danych, którego chcesz użyć do aprowizowania maszyny wirtualnej. Kliknij przycisk **Dalej**.

    ![](./media/data-box-gateway-deploy-provision-vmware/image12.png)
16. Na stronie **Customize settings** (Dostosowywanie ustawień) ustaw wartość **CPU** (Procesor CPU) na 4, **Memory** (Pamięć) na co najmniej 8192 MB, a **Hard disk 1** (Dysk twardy 1) na co najmniej 2 TB. Wybierz **dysk twardy SCSI** do dodania. W tym przypadku był to typ LSI Logic SAS. **Statyczne dyski IDE nie są obsługiwane.** **Hard disk 1** (Dysk twardy 1) jest wirtualnym dyskiem danych. Pamiętaj, że po aprowizowaniu dysku nie można zmniejszyć jego rozmiaru.

    ![](./media/data-box-gateway-deploy-provision-vmware/image13.png)

    Na tej samej stronie kliknij pozycję **Add hard disk** (Dodaj dysk twardy), a następnie wybierz pozycję **Existing hard disk** (Istniejący dysk twardy). Wybierz plik VMDK w magazynie danych. Spowoduje to dodanie dysku systemu operacyjnego. 

     ![](./media/data-box-gateway-deploy-provision-vmware/image14.png)

    Przewiń w dół, aż zobaczysz **nowy dysk twardy** i rozwiń go, aby wyświetlić ustawienia. Ustaw opcję **Virtual Device Node** (Węzeł urządzenia wirtualnego) na wartość **IDE controller 0** (Kontroler IDE 0). Kliknij przycisk **Dalej**.

     ![](./media/data-box-gateway-deploy-provision-vmware/image15.png)

27. Na stronie **Ready to Complete** (Gotowe do ukończenia) przejrzyj wszystkie ustawienia skojarzone z nową maszyną wirtualną. Sprawdź, czy ustawienie procesora CPU ma wartość 4, pamięci — 8192 MB, a interfejsu sieciowego — 1 oraz czy dysk twardy 2 ma wybrany kontroler IDE 0. Kliknij przycisk **Zakończ**. 
   
    ![](./media/data-box-gateway-deploy-provision-vmware/image16.png)
    ![](./media/data-box-gateway-deploy-provision-vmware/image17.png)

Maszyna wirtualna jest teraz aprowizowana. Zostanie wyświetlone odpowiednie powiadomienie, a nowa maszyna wirtualna zostanie dodana do listy maszyn wirtualnych. 

![](./media/data-box-gateway-deploy-provision-vmware/image17.png)

Następnym krokiem jest uruchomienie tej maszyny i uzyskanie adresu IP.

> [!NOTE]
> Nie zalecamy instalowania narzędzi VMware na urządzeniu wirtualnym (aprowizowanym zgodnie z powyższymi informacjami). Zainstalowanie narzędzi VMware spowoduje powstanie nieobsługiwanej konfiguracji.

## <a name="start-the-virtual-device-and-get-the-ip"></a>Uruchamianie urządzenia wirtualnego i uzyskiwanie adresu IP

Wykonaj poniższe kroki, aby uruchomić urządzenie wirtualne i nawiązać z nim połączenie.

#### <a name="to-start-the-virtual-device"></a>Aby uruchomić urządzenie wirtualne
1. Uruchom urządzenie wirtualne. W okienku po prawej stronie wybierz urządzenie z listy maszyn wirtualnych, a następnie kliknij prawym przyciskiem myszy, aby wyświetlić menu kontekstowe. Wybierz pozycję **Power** (Zasilanie), a następnie pozycję **Power on** (Włącz). Maszyna wirtualna powinna zostać włączona. Stan możesz zobaczyć w dolnym okienku klienta internetowego.

    ![](./media/data-box-gateway-deploy-provision-vmware/image19.png)

2. Ponownie wybierz maszynę wirtualną. Kliknij prawym przyciskiem myszy i wybierz polecenie **Console** (Konsola), a następnie **Open in a new window** (Otwórz w nowym oknie).

    ![](./media/data-box-gateway-deploy-provision-vmware/image20.png)

3. Konsola maszyny wirtualnej zostanie otwarta w nowym oknie. 

    ![](./media/data-box-gateway-deploy-provision-vmware/image21.png)

4. Po uruchomieniu urządzenia wskaż i kliknij kartę w górnej, środkowej części okna konsoli. Wybierz pozycję **Guest OS > Send keys > Ctrl+Alt+Delete** (System operacyjny gościa > Wyślij klawisze > Ctrl+Alt+Delete). Spowoduje to odblokowanie maszyny wirtualnej.

   ![](./media/data-box-gateway-deploy-provision-vmware/image22.png)

5. Podaj hasło, aby zalogować się do maszyny. Domyślne hasło to Password1.

   ![](./media/data-box-gateway-deploy-provision-vmware/image23.png)

6. Kroki od 5 do 7 mają zastosowanie tylko w przypadku uruchamiania w środowisku bez protokołu DHCP. W przypadku środowiska z protokołem DHCP pomiń te kroki i przejdź do kroku 8. Jeśli urządzenie zostało uruchomione w środowisku bez protokołu DHCP, zostanie wyświetlony komunikat z taką informacją: **Skonfiguruj sieć za pomocą polecenia cmdlet Set-HcsIPAddress**. 
   
7. Aby skonfigurować sieć, w wierszu polecenia wydaj polecenie `Get-HcsIpAddress` w celu wyświetlenia listy interfejsów sieciowych włączonych na urządzeniu wirtualnym. Jeśli urządzenie ma włączony jeden interfejs sieciowy, jego domyślną nazwą jest `Ethernet`.

8. Skonfiguruj sieć za pomocą polecenia cmdlet `Set-HcsIpAddress`. Przykład przedstawiono poniżej:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

9. Po zakończeniu początkowej konfiguracji i uruchomieniu urządzenia zobaczysz tekst baneru urządzenia. Zanotuj adresy IP i URL wyświetlane w tekście baneru. Posłużą one do zarządzania urządzeniem. Za pomocą tego adresu IP nawiążesz połączenie z internetowym interfejsem użytkownika urządzenia wirtualnego oraz dokończysz lokalną konfigurację i aktywację urządzenia.

   ![](./media/data-box-gateway-deploy-provision-vmware/image24.png)

Jeśli urządzenie nie spełnia minimalnych wymagań dotyczących konfiguracji, w tekście baneru zostanie wyświetlony błąd (widoczny poniżej). Trzeba zmodyfikować konfigurację urządzenia tak, aby zapewnić zasoby spełniające minimalne wymagania. Następnie możesz ponownie uruchomić urządzenie i połączyć się z nim. Minimalne wymagania konfiguracji opisano w sekcji [Sprawdzanie, czy system hosta spełnia minimalne wymagania dotyczące urządzenia wirtualnego](#check-the-host-system).

<!---If you face any other error during the initial configuration using the local web UI, refer to the following workflows:

* Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).-->

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono zagadnienia dotyczące usługi Data Box Gateway, takie jak:

> [!div class="checklist"]
> * Sprawdzanie, czy host spełnia minimalne wymagania dotyczące urządzenia
> * Aprowizowanie urządzenia wirtualnego w programie VMware
> * Uruchamianie urządzenia wirtualnego i uzyskiwanie adresu IP

Przejdź do następnego samouczka, aby dowiedzieć się, jak nawiązać połączenie z urządzeniem wirtualnym oraz skonfigurować i aktywować je.

* [Set up and connect to shares on your Data Box Gateway (Konfigurowanie udziałów w usłudze Data Box Gateway i łączenie się z nimi)](data-box-gateway-deploy-connect-setup-activate.md)

