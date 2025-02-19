# Struktūros: objektų masyvai (skaičiavimai)

## Vaizdo pamoka

Informacija ruošiama.

## Pavyzdžiai

### Pavyzdys 1

Kodas:

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

struct zmogus
{
    string vardas;
    string pavarde;
    int amzius;
    double ugis;

    zmogus(string vardas, string pavarde, int amzius, double ugis)
    {
        this->vardas = vardas;
        this->pavarde = pavarde;
        this->amzius = amzius;
        this->ugis = ugis;
    }

    void isvedimas(string komentaras)
    {
        cout << komentaras << endl;
        cout << vardas << " " << pavarde
            << " (" << amzius << " m.) yra "
            << ugis << " m. ugio.\n\n";
    }
};

void isvedimas(string komentaras, zmogus zmones[], int kiekis)
{
    cout << komentaras << endl;
    cout << "-----------------------------------------\n";
    cout << "Vardas, pavarde        Amzius     Ugis, m\n";
    cout << "-----------------------------------------\n";

    for (int i = 0; i < kiekis; i++)
    {
        cout << setw(22) << left << zmones[i].vardas << " "
            << setw(10) << zmones[i].amzius << " "
            << zmones[i].ugis << endl;
    }

    cout << "-----------------------------------------\n\n";
}

zmogus vyriausias_zmogus(zmogus zmones[], int kiek)
{
    zmogus vyriausias = zmones[0];

    for (int i = 0; i < kiek; i++)
    {
        if (zmones[i].amzius > vyriausias.amzius)
        {
            vyriausias = zmones[i];
        }
    }

    return vyriausias;
}

zmogus zemiausias_zmogus(zmogus zmones[], int kiek)
{
    zmogus zemiausias = zmones[0];

    for (int i = 0; i < kiek; i++)
    {
        if (zmones[i].ugis < zemiausias.ugis)
        {
            zemiausias = zmones[i];
        }
    }

    return zemiausias;
}

double ugiu_suma(zmogus zmones[], int kiek)
{
    double suma = 0;

    for (int i = 0; i < kiek; i++)
    {
        suma += zmones[i].ugis;
    }

    return suma;
}

double ugiu_vidurkis(zmogus zmones[], int kiekis)
{
    return ugiu_suma(zmones, kiekis) / kiekis;
}

int main()
{
    zmogus zmones[] = {
        zmogus("Tomas", "Tomauskas", 23, 1.8),
        zmogus("Giedrius", "Giedriauskas", 25, 1.75),
        zmogus("Inga", "Ingauskiene", 24, 1.67),
        zmogus("Paulina", "Povilaityte", 20, 1.7),
        zmogus("Ignas", "Ignauskas", 19, 1.9)
    };

    int kiekis = 5;

    isvedimas("Pradiniai duomenys", zmones, kiekis);

    zmogus vyriausias = vyriausias_zmogus(zmones, kiekis);
    vyriausias.isvedimas("Vyriausias(-ia) zmogus");

    zemiausias_zmogus(zmones, kiekis).isvedimas("Zemiausias(-ia) zmogus");

    cout << "Ugiu suma: " << ugiu_suma(zmones, kiekis) << " m.\n\n";

    cout << "Ugiu vidurkis: " << ugiu_vidurkis(zmones, kiekis) << " m.\n\n";

    return 0;
}
```

Rezultatai:

```
Pradiniai duomenys
-----------------------------------------
Vardas, pavarde        Amzius     Ugis, m
-----------------------------------------
Tomas                  23         1.8
Giedrius               25         1.75
Inga                   24         1.67
Paulina                20         1.7
Ignas                  19         1.9
-----------------------------------------

Vyriausias(-ia) zmogus
Giedrius Giedriauskas (25 m.) yra 1.75 m. ugio.

Zemiausias(-ia) zmogus
Inga Ingauskiene (24 m.) yra 1.67 m. ugio.

Ugiu suma: 8.82 m.

Ugiu vidurkis: 1.764 m.
```

### Pavyzdys 2

Kodas:

```cpp
#include <iostream>
using namespace std;

struct preke
{
    string pavadinimas;
    double kaina;
    double savikaina;
    int kiekis;

    preke(string pavadinimas, double kaina, double savikaina, int kiekis)
    {
        this->pavadinimas = pavadinimas;
        this->kaina = kaina;
        this->savikaina = savikaina;
        this->kiekis = kiekis;
    }

    void isvedimas()
    {
        cout << "Pavadinimas: " << pavadinimas << endl
            << "Kaina: " << kaina << " eur\n"
            << "Savikaina: " << savikaina << " eur\n"
            << "Kiekis: " << kiekis << " vnt.\n\n";
    }

    double pelningumas()
    {
        return (kaina - savikaina) * kiekis;
    }
};

void isvedimas(preke prekes[], int kiek)
{
    cout << "-------------------\n\n";

    for (int i = 0; i < kiek; i++)
    {
        cout << i + 1 << "-oji preke:\n\n";
        prekes[i].isvedimas();
    }

    cout << "-------------------\n\n";
}

preke didziausias_pelnas(preke prekes[], int kiek)
{
    preke did = prekes[0];

    for (int i = 0; i < kiek; i++)
    {
        if ((prekes[i].kaina - prekes[i].savikaina) > (did.kaina - did.savikaina))
        {
            did = prekes[i];
        }
    }

    return did;
}

int maziausias_kiekis(preke prekes[], int kiek)
{
    int maz = prekes[0].kiekis;

    for (int i = 0; i < kiek; i++)
    {
        if (prekes[i].kiekis < maz)
        {
            maz = prekes[i].kiekis;
        }
    }

    return maz;
}

preke pelningiausia_preke(preke prekes[], int kiek)
{
    preke pelningiausia = prekes[0];

    for (int i = 0; i < kiek; i++)
    {
        if (prekes[i].pelningumas() > pelningiausia.pelningumas())
        {
            pelningiausia = prekes[i];
        }
    }
    
    return pelningiausia;
}

int prekiu_kiekis_kuriu_daugiau_nei(preke prekes[], int kiekis, int daugiau_nei)
{
    int atrinktu_kiekis = 0;

    for (int i = 0; i < kiekis; i++)
    {
        if (prekes[i].kiekis > daugiau_nei)
        {
            atrinktu_kiekis++;
        }
    }

    return atrinktu_kiekis;
}

void skaiciavimai(preke prekes[], int kiekis)
{
    cout << "Didziausias pelnas (kaina - savikaina):\n\n";
    preke didz_pelnas = didziausias_pelnas(prekes, kiekis);
    didz_pelnas.isvedimas();
    cout << "Paskaiciuotas pelnas: "
        << didz_pelnas.kaina - didz_pelnas.savikaina << " eur\n\n";

    cout << "-------------------\n\n";

    cout << "Maziausias kiekis: " << maziausias_kiekis(prekes, kiekis)
        << " vnt.\n\n";

    cout << "-------------------\n\n";

    cout << "Pelningiausia preke (pardavus visus vnt, skaiciuojant pelna):\n\n";
    preke pelning = pelningiausia_preke(prekes, kiekis);
    pelning.isvedimas();
    cout << "Jos galimas pelningumas: " << pelning.pelningumas() << " eur\n\n";

    cout << "-------------------\n\n";

    cout << "Prekiu kiekis, kuriu daugiau nei 100 vnt.: "
        << prekiu_kiekis_kuriu_daugiau_nei(prekes, kiekis, 100) << "\n\n";

    cout << "-------------------\n\n";
}

int main()
{
    preke prekes[] = {
        preke("Dzemperis", 24.99, 10, 45),
        preke("Juodos kelnes", 15.99, 8, 158),
        preke("Sportbaciai", 26.49, 12.87, 215),
        preke("Kepure", 4.99, 2.5, 8),
        preke("Basutes", 3.49, 2.1, 78),
    };

    int kiekis = 5;

    isvedimas(prekes, kiekis);
    skaiciavimai(prekes, kiekis);

    return 0;
}
```

Rezultatai:

```
-------------------

1-oji preke:

Pavadinimas: Dzemperis
Kaina: 24.99 eur
Savikaina: 10 eur
Kiekis: 45 vnt.

2-oji preke:

Pavadinimas: Juodos kelnes
Kaina: 15.99 eur
Savikaina: 8 eur
Kiekis: 158 vnt.

3-oji preke:

Pavadinimas: Sportbaciai
Kaina: 26.49 eur
Savikaina: 12.87 eur
Kiekis: 215 vnt.

4-oji preke:

Pavadinimas: Kepure
Kaina: 4.99 eur
Savikaina: 2.5 eur
Kiekis: 8 vnt.

5-oji preke:

Pavadinimas: Basutes
Kaina: 3.49 eur
Savikaina: 2.1 eur
Kiekis: 78 vnt.

-------------------

Didziausias pelnas (kaina - savikaina):

Pavadinimas: Dzemperis
Kaina: 24.99 eur
Savikaina: 10 eur
Kiekis: 45 vnt.

Paskaiciuotas pelnas: 14.99 eur

-------------------

Maziausias kiekis: 8 vnt.

-------------------

Pelningiausia preke (pardavus visus vnt, skaiciuojant pelna):

Pavadinimas: Sportbaciai
Kaina: 26.49 eur
Savikaina: 12.87 eur
Kiekis: 215 vnt.

Jos galimas pelningumas: 2928.3 eur

-------------------

Prekiu kiekis, kuriu daugiau nei 100 vnt.: 2

-------------------
```

## Užduotys

Informacija ruošiama.
