from random import randint, choice

hp = 100 
uratowane_miasto = False
pokonanych_zagrozen = 0

def losowe_zdarzenia():
    zdazenia = [
        {"name": "Bandyta", "damage": randint(10, 20)},
        {"name": "Pożar", "damage": randint(5, 15)},
        {"name": "Eksplozja", "damage": randint(8, 18)}
    ]
    return choice(zdazenia)

print("Witaj w grze! Twoim zadaniem jest uratować miasto przed katastrofą.")
print("Uważaj! Jeśli twoje życie spadnie do zera, przegrasz.")
print("Pokonaj 5 zagrożeń, aby uratować miasto!\n")

while hp > 0 and not uratowane_miasto:
    zdazenia = losowe_zdarzenia()
    print(f"Zagrożenie: {zdazenia['name']}! Może zadać do {zdazenia['damage']} obrażeń.")
    print("Co chcesz zrobić?")
    print("1. Walcz")
    print("2. Uciekaj")
    print("3. Odpocznij")
    
    decyzje_gracza = input("Wybierz (1/2/3): ")  
    
    if decyzje_gracza == "1":
        uszkodzenie_przeciwnika = randint(10, 25) 
        uszkodzenie_gracza = zdazenia["damage"] 
        print(f"Zadałeś {uszkodzenie_przeciwnika} obrażeń {zdazenia['name']}!")
        print(f"Otrzymałeś {uszkodzenie_gracza} obrażeń podczas walki.")
        hp -= uszkodzenie_gracza
        pokonanych_zagrozen += 1
        print(f"ilosc pokonanych zagrozen {pokonanych_zagrozen} ")
    elif decyzje_gracza == "2":
        ucieczka_od_uszkodzen = randint(5, 10)
        print(f"Udało ci się uciec, ale straciłeś {ucieczka_od_uszkodzen} punktów życia z wyczerpania.")
        hp -= ucieczka_od_uszkodzen
    elif decyzje_gracza == "3":
        heal = randint(3, 9)
        print(f"Odpocząłeś i odzyskałeś {heal} punktów życia.")
        hp += heal
        hp = min(hp, 100)  
    else:
        print("Nieprawidłowy wybór, tracisz turę!")
    
    print(f"Twoje aktualne życie: {hp}\n")
    
    if pokonanych_zagrozen >= 5:
        uratowane_miasto = True
        print("Gratulacje! Pokonałeś wszystkie zagrożenia i uratowałeś miasto!")
    elif hp <= 0:
        print("Twoje życie spadło do zera. Miasto zostało zniszczone... Przegrałeś.")

print("Dziękujemy za grę!")
