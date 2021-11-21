# PRiR_LAB5_1

Zadanie 1 z laboratoriów 5 z przedmiotu PRiR.
Program napisany w języku c liczy całkę 4*x-6*x+5 na p procesach wykorzystując fork(). 
Każdy proces ma inny przedział <a,b> który jest losowany. Każdy proces ma swoje orginalne ziarno. Program liczy dla dwóch metod(trapezów i kwadratury Gaussa).

Opis kodu:

main tu użytkownik jest pytany o liczbę procesów a następnie w pętli for dla każdego procesu sprawdzany jest czy fork() jest równe 0 oraz ustawiane jest zairono oraz losowany zakres przedziału i n. Następnie wywoływane sąfunkcje liczące wartość całki używając odpowiednich metod.

    int main() {
      int liczbaProcesow, a, b, n;
        printf("Podaj ile ma byc procesow: ");
        scanf("%d", &liczbaProcesow);

    int p;
    printf("Metoda trapezow\n ");
      for(p = 0 ; p < liczbaProcesow; p++) {
          if(fork() == 0) {
              srand(p + 1);

              a = rand() % 31;
              b =  (a + 1) + rand() % 29;
              n = 10 + rand() % 91;

              printf("Metoda trapezow ||| Liczba trapezow = $d | a = $d | b = $d | wynik = %f | numer procesu = %d\n", n, a, b, trapezy(a, b, n), p);

        n = 1 + rand() % 10;		
              printf("Metoda kwadratury ||| a = $d | b = $d | wynik = %f | numer procesu = %d\n", a, b, kwadratura(a, b, n), p);
              exit(0);
          }
      }
    }
    
funkcja licząca wartość dla podanego wzoru.
    
    float f_x(float x) {
        return 4 * x - 6 * x + 5;
    }
    
funckja licząca wartość całki na podstawie metody trapezów.

    float trapezy(int a, int b, int n) {
        float h = (float)(b - a) / n;
        float suma = 0;

      int i;
        for(i = 1; i < n; i++) {
        suma += f_x(a + i * h);
      }
      suma += f_x(a) / 2;
      suma += f_x(b) / 2;

      return h * suma;
    }
    
Metoda licząca wartość całki metodą kwadratury Gaussa.

    float kwadratura(int a, int b, int n) {
            double w = 0.0,t,pom1,pom2;
            pom1 = (double)(b - a) / 2;
            pom2 = (double)(b + a) / 2;
        if(n % 2 != 0) {
          n++;
        }
        switch(n) {
          case 2: {
                    double tab[][] = {1.0000000000000000,-0.5773502691896257}, {1.0000000000000000,0.5773502691896257}};
                }break;
          case 4: {
                    double tab[][] = {{0.6521451548625461,-0.3399810435848563}, {0.6521451548625461,0.3399810435848563},
                    {0.3478548451374538,-0.8611363115940526}, {0.3478548451374538,0.8611363115940526}};
                }break;
          case 6: {
                    double tab[][] = {0.3607615730481386,0.6612093864662645}, {0.3607615730481386,-0.6612093864662645},
                    {0.4679139345726910,-0.2386191860831969}, {0.4679139345726910,0.2386191860831969},
                    {0.1713244923791704,-0.9324695142031521}, {0.1713244923791704,0.9324695142031521}};
                }break;
          case 8: {
                    double tab[][] = {{0.3626837833783620,-0.1834346424956498}, {0.3626837833783620,0.1834346424956498},
                    {0.3137066458778873,-0.5255324099163290}, {0.3137066458778873,0.5255324099163290},
                    {0.2223810344533745,-0.7966664774136267}, {0.2223810344533745,0.7966664774136267},
                    {0.1012285362903763,-0.9602898564975363}, {0.1012285362903763,0.9602898564975363}};
                }break;
          case 10: {
                    double tab[][] = {{0.2955242247147529,-0.1488743389816312}, {0.2955242247147529,0.1488743389816312},
                    {0.2692667193099963,-0.4333953941292472}, {0.2692667193099963,0.4333953941292472},
                    {0.2190863625159820,-0.6794095682990244}, {0.2190863625159820,0.6794095682990244},
                    {0.1494513491505806,-0.8650633666889845}, {0.1494513491505806,0.8650633666889845},
                    {0.0666713443086881,-0.9739065285171717}, {0.0666713443086881,0.9739065285171717}};
                }break;
          default:
          double tab[][];
        }

        int i;
            for(i = 0; i < n; i++) {
                t = 0.0;
                t = pom1 * tab[i][1] + pom2;
                w += tab[i][0] * f_x(t);
            }

            return (float)w;
        }
