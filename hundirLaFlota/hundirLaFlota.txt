package hundirlaflotaremastered;
import java.util.InputMismatchException;
import java.util.Random;
import java.util.Scanner;
;
public class HundirLaFlotaRemastered {
    public static final String ANSI_RED = "\u001B[31m"; //color rojo
    public static final String ANSI_RESET = "\u001B[0m"; //reset de color
    public static final String ANSI_BLUE = "\u001B[34m"; //color azul
    public static final String ANSI_YELLOW = "\u001B[33m"; //color amarillo
    public static void limpiarPantalla() { //funcion para limpiar la pantalla  
        for (int i = 0; i < 50; ++i) System.out.println(); 
    } 
    public static int escribirFila(){
        Scanner lector = new Scanner(System.in);
        System.out.println("\n" + "Escriba la fila.");
        int coordenadaFila = lector.nextInt(); 
        while(coordenadaFila < 1 || coordenadaFila > 10){ //bucle error fila
            System.out.println("\n" + "Fila incorrecta." + "\n" + "Vuelva a introducir la fila." + "\n");
            coordenadaFila = lector.nextInt(); 
        }
        return coordenadaFila;
    }
    public static int escribirColumna(){
        Scanner lector = new Scanner(System.in);
        System.out.println("\n" + "Ahora escriba la columna.");
        char coordenadaLetra = lector.next().charAt(0); 
        coordenadaLetra = Character.toUpperCase(coordenadaLetra); //cambio a mayusculas la letra introducida
        String letra = Character.toString(coordenadaLetra); //transformo a string la letra(char)
        boolean letraAceptada = letraCorrecta(letra); //le mando ese string a la funcion soloAlfabeto que me combruba si la letra está entre la A y la J y me devuelve true o false
        while(!letraAceptada ){ //error si la letra no está entra la A y la J
            System.out.println("\n" + "Columna incorrecta." + "\n" + "Vuelva a introducir la columna." + "\n");
            coordenadaLetra = lector.next().charAt(0);
            coordenadaLetra = Character.toUpperCase(coordenadaLetra); //me pone la letra de la columna en mayuscula
            letra = Character.toString(coordenadaLetra); //la variable l es la que almacena la coordenada pero convertida en string
            letraAceptada = letraCorrecta(letra); //en la variable letraCorrecta almaceno true o false
        }
        char letrasMayusculas [] = new char [11]; //array de letras para transformar la letra en numero
        char letraMayuscula = '@'; 
        int coordenadaColumna = 0;
        for (int i = 0; i < letrasMayusculas.length; i++) { //bucle que transforma la letra en numero de columna
            letrasMayusculas[i]=letraMayuscula;
            if(coordenadaLetra == letrasMayusculas[i]){
                coordenadaColumna = i;
            }
            letraMayuscula++; //incrementa letra
        }
        return coordenadaColumna;
    }
    public static boolean letraCorrecta(String cadena){
        String letras = "^[A-J]*$";
        return cadena.matches(letras);  //retorna true o false según coincida o no con el string letras
    }
    public static int menuTirada(){
        Scanner lector = new Scanner (System.in);
        int opcion = 0;
        while(opcion>4 || opcion<1){
            try{
                System.out.println("\n" + "Tu turno. ¿Qué quieres hacer?" + "\n");
                System.out.println("1- Atacar.");
                System.out.println("2- Guardar.");
                System.out.println("3- Guardar y salir.");
                System.out.println("4- Salir.");
                opcion = lector.nextInt();
            }catch(InputMismatchException e){
                System.out.println("\n"+"Debes escribir una opción válida.");
                lector.next();
            }
        }
        return opcion;
    }
    public static void mostrarTableroJugador1(String tableroJugador[][]){
        //System.out.println("\n" + "\n"+ "Tu tablero" + ANSI_BLUE + " de barcos:" + ANSI_RESET + "\n");
        for(int fila = 0; fila < tableroJugador.length; fila++) { //con este bucle se genera el tablero
            System.out.print("|");
            for (int columna = 0; columna < tableroJugador.length; columna++) {
                if(fila==10 && columna==0){
                    System.out.print("10|");  
                }else{
                    System.out.print(tableroJugador[fila][columna]+"|");
                }
            }
            System.out.println("");
        }
    }
    public static void barcosManual(String tablero[][]){ 
        Scanner lector=new Scanner(System.in);
        String [] letrasBarcos = {"P1", "S1", "S2", "F1", "F2", "F3", "L1", "L2", "L3", "L4"};
        int opcionColocar=0;
        int contadorBarcosColocados=0;
        int tamanno=0;
        int contadorArrayBarcos=0;
        String [] barcos = {"1 porta-avión.", "2 submarinos.", "1 submarino.", "3 fragatas.", "2 fragatas.", "1 fragata.", "4 lanchas.", "3 lanchas.", "2 lanchas.", "1 lancha."};  
        limpiarPantalla();
        while(contadorBarcosColocados<6){
            if(contadorBarcosColocados==0){ //si es el portaavion
                tamanno=4;
            }else if(contadorBarcosColocados>0 && contadorBarcosColocados<3){ //si es submarino
                tamanno=3;
            }else if(contadorBarcosColocados>2 && contadorBarcosColocados<6){ //si es fragata
                tamanno=2;
            }else{ //si es lancha
                tamanno=1;
            }
            limpiarPantalla();
            mostrarTableroJugador1(tablero);
                while(opcionColocar<1 || opcionColocar>4){
                    try{
                        System.out.println("\n"+"\n"+"Te toca colocar "+barcos[contadorBarcosColocados]+"\n"+"¿Cómo quieres colocarlo? Elige una opción correcta."+"\n");
                        System.out.println("1- Horizontal.");
                        System.out.println("2- Vertical.");
                        System.out.println("3- Diagonal hacia la decrecha.");
                        System.out.println("4- Diagonal hacia la izquierda.");
                        opcionColocar=lector.nextInt();
                    }catch(InputMismatchException e){
                        System.out.println("\n"+"Debes escribir una opción válida.");
                        lector.next();
                    } 
                }
                limpiarPantalla();
                mostrarTableroJugador1(tablero);
                switch(opcionColocar){ //segun que opcion de colocar elija
                    case 1:{ //horizontal
                        System.out.println("\n"+"Ha seleccionado horizontal.");
                        break;  
                    }
                    case 2:{ //vertical
                        System.out.println("\n"+"Ha seleccionado vertical.");
                        break;
                    }
                    case 3:{ //diagonal derecha
                        System.out.println("\n"+"Ha seleccionado diagonal derecha.");
                        break;
                    }
                    case 4:{ //diagonal izquierda
                        System.out.println("\n"+"Ha seleccionado diagonal izquierda.");
                        break;
                    }
                }
                comprobarBarco(tablero, tamanno, opcionColocar, contadorBarcosColocados);
                contadorBarcosColocados++;
                opcionColocar=0;
        }
        while(contadorBarcosColocados>5 && contadorBarcosColocados<10){
            limpiarPantalla();
            mostrarTableroJugador1(tablero);
            System.out.println("\n"+"\n"+"Te toca colocar "+barcos[contadorBarcosColocados]);
            int fila=escribirFila();
            int columna=escribirColumna();
            tablero[fila][columna]=letrasBarcos[contadorBarcosColocados];
            contadorBarcosColocados++;
        }
    }
    public static void barcosAuto(String tablero[][]){
        int tamanno=0;
        int contadorBarcosColocados=0;
        Random numeroAleatio = new Random();
        while(contadorBarcosColocados<9){
            if(contadorBarcosColocados==0){ //si es el portaavion
                tamanno=4;
            }else if(contadorBarcosColocados>0 && contadorBarcosColocados<3){ //si es submarino
                tamanno=3;
            }else if(contadorBarcosColocados>2 && contadorBarcosColocados<6){ //si es fragata
                tamanno=2;
            }else{ //si es lancha
                tamanno=1;
            }
            boolean correcto=false;
            boolean choque=true;
            int contadorCasillasLibres=0;
            int posicionRandom = numeroAleatio.nextInt(4)+1;
            int fila = 0;
            int columna = 0;
            switch(posicionRandom){
                case 1:{ //horizontal
                    while(choque){
                        fila =  numeroAleatio.nextInt(10)+1;
                        columna = numeroAleatio.nextInt(10-tamanno)+1;
                        int filaVariable = fila;
                        int columnaVariable = columna;
                        for (int i = 0; i < tamanno; i++) {
                            if(tablero[filaVariable][columnaVariable].equals("  ")){
                                contadorCasillasLibres++;
                                columnaVariable++;
                            } 
                        }
                        if(contadorCasillasLibres==tamanno){
                            choque=false;
                        }else{
                            contadorCasillasLibres=0;
                        }
                    }
                    break;
                }
                case 2:{ //vertical
                    while(choque){
                        fila =  numeroAleatio.nextInt(10-tamanno)+1;
                        columna = numeroAleatio.nextInt(10)+1;
                        int filaVariable = fila;
                        int columnaVariable = columna;
                        for (int i = 0; i < tamanno; i++) {
                            if(tablero[filaVariable][columnaVariable].equals("  ")){
                                contadorCasillasLibres++;
                                filaVariable++;
                            } 
                        }
                        if(contadorCasillasLibres==tamanno){
                            choque=false;
                        }else{
                            contadorCasillasLibres=0;
                        }
                    }
                    break;
                }
                case 3:{ //diagonal derecha
                    while(choque){
                        fila =  numeroAleatio.nextInt(10-tamanno)+1;
                        columna = numeroAleatio.nextInt(10-tamanno)+1;
                        int filaVariable = fila;
                        int columnaVariable = columna;
                        for (int i = 0; i < tamanno; i++) {
                            if(tablero[filaVariable][columnaVariable].equals("  ")){
                                contadorCasillasLibres++;
                                filaVariable++;
                                columnaVariable++;
                            } 
                        }
                        if(contadorCasillasLibres==tamanno){
                            choque=false;
                        }else{
                            contadorCasillasLibres=0;
                        }
                    }
                    break;
                }
                case 4:{ //diagonal izquierda
                    while(choque){
                        fila =  numeroAleatio.nextInt(10-tamanno)+1;
                        columna = numeroAleatio.nextInt(10-tamanno)+1;
                        int filaVariable = fila;
                        int columnaVariable = columna;
                        for (int i = 0; i < tamanno; i++) {
                            if(tablero[filaVariable][columnaVariable].equals("  ")){
                                contadorCasillasLibres++;
                                filaVariable++;
                                columnaVariable--;
                            } 
                        }
                        if(contadorCasillasLibres==tamanno){
                            choque=false;
                        }else{
                            contadorCasillasLibres=0;
                        }
                    }
                    break;
                }
            }
            colocar(tablero, fila, columna, tamanno, posicionRandom, contadorBarcosColocados); 
            contadorBarcosColocados++;    
        }
    }
    public static void comprobarBarco(String tablero[][], int tamanno, int posicion, int contadorBarcosColocados){
        int fila=escribirFila();
        int columna=escribirColumna();
        int columnaVariable=columna;
        int filaVariable=fila;
        int contadorCasillasLibres=0;
        boolean choque=true;
        boolean correcto=false;
        limpiarPantalla();
        switch(posicion){ //comprueba el barco según la posicion
            case 1:{ //horizontal
                while(!correcto){ //bucle del que solo se sale cuando se compruebe que se puede colocar ahí
                    for (int i = 0; i < tamanno; i++) {
                        if(tablero[filaVariable][columnaVariable].equals("  ")){
                            contadorCasillasLibres++;
                            columnaVariable++;
                        }
                    }    
                    if(contadorCasillasLibres==tamanno){
                        choque=false;
                    }
                    if(columna + tamanno-1 > 10 || choque ){
                        System.out.println("\n"+"El barco no puede colocarse ahí. Deberás volver a introducir unas coordenadas."+"\n");
                        fila=escribirFila();
                        columna=escribirColumna();
                        filaVariable=fila;
                        columnaVariable=columna;
                        contadorCasillasLibres=0;
                    }else{
                        correcto=true;
                    }
                }
                break;
            }
            case 2:{ //vertical
                while(!correcto){ //bucle del que solo se sale cuando se compruebe que se puede colocar ahí
                    for (int i = 0; i < tamanno; i++) {
                        if(tablero[filaVariable][columnaVariable].equals("  ")){
                            contadorCasillasLibres++;
                            filaVariable++;
                        }
                    }    
                    if(contadorCasillasLibres==tamanno){
                        choque=false;
                    }
                    if(fila + tamanno-1 > 10 || choque ){
                        mostrarTableroJugador1(tablero);
                        System.out.println("\n"+"El barco no puede colocarse ahí. Deberás volver a introducir otras coordenadas."+"\n");
                        fila=escribirFila();
                        columna=escribirColumna();
                        filaVariable=fila;
                        columnaVariable=columna;
                        contadorCasillasLibres=0;
                    }else{
                        correcto=true;
                    }
                }
                break;
            }
            case 3:{ //diagonal derecha
                while(!correcto){ //bucle del que solo se sale cuando se compruebe que se puede colocar ahí
                    for (int i = 0; i < tamanno; i++) {
                        if(tablero[filaVariable][columnaVariable].equals("  ")){
                            contadorCasillasLibres++;
                            filaVariable++;
                            columnaVariable++;
                        }
                    }    
                    if(contadorCasillasLibres==tamanno){
                        choque=false;
                    }
                    if(fila + tamanno-1 > 10 || columna + tamanno-1 > 10 || choque ){
                        System.out.println("\n"+"El barco no puede colocarse ahí. Deberás volver a introducir otras coordenadas."+"\n");
                        fila=escribirFila();
                        columna=escribirColumna();
                        filaVariable=fila;
                        columnaVariable=columna;
                        contadorCasillasLibres=0;
                    }else{
                        correcto=true;
                    }
                }
                break;
            }
            case 4:{ //diagonal izquierda
                while(!correcto){ //bucle del que solo se sale cuando se compruebe que se puede colocar ahí
                    for (int i = 0; i < tamanno; i++) {
                        if(tablero[filaVariable][columnaVariable].equals("  ")){
                            contadorCasillasLibres++;
                            filaVariable++;
                            columnaVariable--;
                        }
                    }    
                    if(contadorCasillasLibres==tamanno){
                        choque=false;
                    }
                    if(fila + tamanno-1 > 10 || columna - (tamanno-1) < 1 || choque ){
                        System.out.println("\n"+"El barco no puede colocarse ahí. Deberás volver a introducir otras coordenadas."+"\n");
                        fila=escribirFila();
                        columna=escribirColumna();
                        filaVariable=fila;
                        columnaVariable=columna;
                        contadorCasillasLibres=0;
                    }else{
                        correcto=true;
                    }
                }
                break;
            }
        }
        //una vez comprobada la posicion, se coloca el barco
        colocar(tablero, fila, columna, tamanno, posicion, contadorBarcosColocados); 
    }
    public static void colocar(String tablero [][], int fila, int columna, int tamanno, int posicion, int contadorBarcosColocados){
        String [] letrasBarcos = {"P1", "S1", "S2", "F1", "F2", "F3", "L1", "L2", "L3", "L4"};
        switch(posicion){
            case 1:{ //horizontal
                for (int i = 0; i < tamanno; i++) {
                    tablero[fila][columna]=letrasBarcos[contadorBarcosColocados];
                    columna++;
                }
                break;
            }
            case 2:{ //vertical
                for (int i = 0; i < tamanno; i++) {
                    tablero[fila][columna]=letrasBarcos[contadorBarcosColocados];
                    fila++;
                }
                break;
            }
            case 3:{
                for (int i = 0; i < tamanno; i++) {
                    tablero[fila][columna]=letrasBarcos[contadorBarcosColocados];
                    fila++;
                    columna++;
                }
                break;
            }
            case 4:{
                for (int i = 0; i < tamanno; i++) {
                    tablero[fila][columna]=letrasBarcos[contadorBarcosColocados];
                    fila++;
                    columna--;
                }
                break;
            }
        }
    }
    public static void main(String[] args) {
        Scanner lector=new Scanner(System.in); //defino un scanner
        String tableroJugador1 [][] = new String [11][11]; //creo la matriz
        //genero el tablero de los barcos del jugador
        char letra = 'A'; //defino la letra para las columnas
        char numero = '1'; //defino el numero para las filas
        tableroJugador1[0][0]="  "; //pongo un espacio en esa posición
        for (int fila = 1; fila < tableroJugador1.length; fila++) { //relleno los numeros de las filas
            if(numero<='9'){
            tableroJugador1[fila][0]=String.valueOf(numero)+" ";
            numero++;    
            }  
        }
        for (int columna = 1; columna < tableroJugador1.length; columna++) { //relleno las letras de las columnas
            tableroJugador1[0][columna]=String.valueOf(letra)+" ";
            letra++;
        }
        for (int fila = 1; fila < tableroJugador1.length; fila++) { //relleno el tablero con espacios
            for (int columna = 1; columna < tableroJugador1.length; columna++) {
                tableroJugador1[fila][columna]="  ";
            } 
        }
        //defino los demás tableros
        //////////////////////////////////////////////////////////////////////////// REVISAR ESTO AL FINAL PARA MOVERLO DE SITIO
        String tableroAtaque1 [][] = new String [11][11];
        String tableroAtaque2 [][] = new String [11][11];
        int opcionMenu = 0;
        while(opcionMenu<1 || opcionMenu>3){ //primer menú
            try{ //uso un try catch para que no se puedan poner letras
                System.out.println("\n"+"Bienvenido a hundir la flota. Elija una opción:"+"\n");
                System.out.println("1- Jugar.");
                System.out.println("2- Ayuda.");
                System.out.println("3- Salir.");
                opcionMenu=lector.nextInt();
            }catch(InputMismatchException e){
                System.out.println("\n"+"Debes escribir una opción válida.");
                lector.next();
            }
        }
        limpiarPantalla();
        switch(opcionMenu){ //opciones del primer menú
            case 1:{ //jugar
                opcionMenu=0;
                while(opcionMenu<1 || opcionMenu>3){ //primer menú
                    try{ //uso un try catch para que no se puedan poner letras
                        System.out.println("\n"+"Has seleccionado jugar. Elige una opción válida."+"\n");
                        System.out.println("1- Nueva partida.");
                        System.out.println("2- Cargar partida.");
                        System.out.println("3- Salir.");
                        opcionMenu=lector.nextInt();
                    }catch(InputMismatchException e){
                        System.out.println("\n"+"Debes escribir una opción válida.");
                        lector.next();
                    }
                }
                limpiarPantalla();
                switch(opcionMenu){ //partida
                    case 1:{ //nueva partida
                        boolean ganador=false;
                        boolean coordenadaRepetida=true;
                        opcionMenu=0;
                        while(opcionMenu<1 || opcionMenu>3){ //primer menú
                            try{ //uso un try catch para que no se puedan poner letras
                                System.out.println("\n"+"Has seleccionado nueva partida. Elige una opción válida."+"\n");
                                System.out.println("1- Colocar barcos manualmente.");
                                System.out.println("2- Colocar barcos automáticamente.");
                                System.out.println("3- Salir.");
                                opcionMenu=lector.nextInt();
                            }catch(InputMismatchException e){
                                System.out.println("\n"+"Debes escribir una opción válida.");
                                lector.next();
                            }
                        }
                        limpiarPantalla();
                        switch(opcionMenu){ //como colocar los barcos
                            case 1:{ //manual
                                opcionMenu=0;
                                barcosManual(tableroJugador1);
                                break;
                            }
                            case 2:{ //automatico
                                barcosAuto(tableroJugador1);
                                limpiarPantalla();
                                break;
                            }
                            case 3:{ //salir
                                break;
                            }
                        }//fin como colocar barcos
                        limpiarPantalla();
                        mostrarTableroJugador1(tableroJugador1);
                        String tableroJugador2 [][] = new String [11][11];
                        letra = 'A'; //defino la letra para las columnas
                        numero = '1'; //defino el numero para las filas
                        tableroJugador2[0][0]="  "; //pongo un espacio en esa posición
                        tableroAtaque1[0][0]= "  ";
                        for (int fila = 1; fila < tableroJugador2.length; fila++) { //relleno los numeros de las filas
                            if(numero<='9'){
                            tableroJugador2[fila][0]=String.valueOf(numero)+" ";
                            tableroAtaque1[fila][0]=String.valueOf(numero)+" ";
                            numero++;    
                            }  
                        }
                        for (int columna = 1; columna < tableroJugador2.length; columna++) { //relleno las letras de las columnas
                            tableroJugador2[0][columna]=String.valueOf(letra)+" ";
                            tableroAtaque1[0][columna]=String.valueOf(letra)+" ";
                            letra++;
                        }
                        for (int fila = 1; fila < tableroJugador2.length; fila++) { //relleno el tablero con espacios
                            for (int columna = 1; columna < tableroJugador2.length; columna++) {
                                tableroJugador2[fila][columna]="  ";
                                tableroAtaque1[fila][columna]="  ";
                            } 
                        }
                        System.out.println("Barcos colocados. La máquina va a colocar sus barcos..."+"\n");
                        barcosAuto(tableroJugador2);
                        System.out.println("La máquina está lista. Comienza la partida.");
                        Random aleatorio = new Random();
                        int contadorTocadosJugador = 0;
                        int contadorTocadosMaquina = 0;
                        int contadorP1Maquina = 0;
                        int contadorS1Maquina = 0;
                        int contadorS2Maquina = 0;
                        int contadorF1Maquina = 0;
                        int contadorF2Maquina = 0;
                        int contadorF3Maquina = 0;        
                        int contadorP1Jugador = 0;
                        int contadorS1Jugador = 0;
                        int contadorS2Jugador = 0;
                        int contadorF1Jugador = 0;
                        int contadorF2Jugador = 0;
                        int contadorF3Jugador = 0;
                        limpiarPantalla();
                        int turno = aleatorio.nextInt(2)+1;
                        while(!ganador){
                            if(turno%2==0){
                                mostrarTableroJugador1(tableroJugador1);
                                System.out.println("");
                                mostrarTableroJugador1(tableroAtaque1);
                                //muestro menu tirada
                                opcionMenu=menuTirada(); 
                                limpiarPantalla();
                                switch(opcionMenu){
                                    case 1:{ //atacar
                                        opcionMenu=0;
                                        while(opcionMenu<1 || opcionMenu>2){ 
                                            try{ //uso un try catch para que no se puedan poner letras
                                                System.out.println("\n"+"Vamos al ataque. ¿Cómo quieres realizar el disparo?"+"\n");
                                                System.out.println("1- Disparo manual.");
                                                System.out.println("2- Disparo aleatorio.");
                                                opcionMenu=lector.nextInt();
                                            }catch(InputMismatchException e){
                                                System.out.println("\n"+"Debes escribir una opción válida.");
                                                lector.next();
                                            }
                                        }
                                        switch(opcionMenu){ //tipo de disparo
                                            case 1:{ //disparo manual
                                                
                                                break;
                                            }
                                            case 2:{ //disparo aleatorio
                                                //////////////////
                                                break;
                                            }
                                        }
                                        limpiarPantalla();
                                        mostrarTableroJugador1(tableroJugador1);
                                        System.out.println("");
                                        mostrarTableroJugador1(tableroAtaque1);
                                        int fila=0;
                                        int columna=0;
                                        if(opcionMenu==1){
                                            do{
                                                System.out.println("\n"+"Escriba fila y columna donde desea disparar.");
                                                fila = escribirFila();
                                                columna = escribirColumna();
                                                //compruebo si la casilla ya se ha dicho anteriormente
                                                if (tableroJugador2[fila][columna]!="AA" && tableroJugador2[fila][columna]!="TT" && tableroJugador2[fila][columna]!="HH"){
                                                    coordenadaRepetida=false;
                                                }else{
                                                    System.out.println("\n" + "Error. Esa casilla ya ha sido dicha.");
                                                }
                                            }while(coordenadaRepetida);
                                        }
                                        if(opcionMenu==2){ 
                                            do{
                                                fila=aleatorio.nextInt(10)+1;
                                                columna=aleatorio.nextInt(10)+1;
                                                    //compruebo si la casilla ya se ha dicho anteriormente
                                                if (tableroJugador2[fila][columna]!="AA" && tableroJugador2[fila][columna]!="TT" && tableroJugador2[fila][columna]!="HH"){
                                                    coordenadaRepetida=false;
                                                }
                                            }while(coordenadaRepetida);
                                        }else{
                                            do{
                                                escribirFila();
                                                escribirColumna();
                                            if (tableroJugador2[fila][columna]!="AA" && tableroJugador2[fila][columna]!="TT" && tableroJugador2[fila][columna]!="HH"){
                                                    coordenadaRepetida=false;
                                                }
                                            }while(coordenadaRepetida);
                                        }
                                        coordenadaRepetida=false;
                                        //pongo tocado, agua o hundido
                                        if(tableroJugador2[fila][columna]!="  "){ //si hay un barco
                                            if(tableroJugador2[fila][columna] == "P1"){ //si hay una P
                                                System.out.println("Lanzamiento del jugador: "+ANSI_YELLOW+"¡PORTAAVION TOCADO!"+ANSI_RESET);
                                                contadorP1Maquina++;
                                                if(contadorP1Maquina == 4){ //poner hundido en portaavion
                                                    System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡PORTAAVION HUNDIDO!"+ANSI_RESET);
                                                    for (int i = 0; i < tableroJugador2.length; i++){
                                                        for (int j = 0; j < tableroJugador2.length; j++) {
                                                            if(tableroJugador2[i][j] == "P1"){
                                                                tableroAtaque1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                            }
                                                        }
                                                    }
                                                }else if(contadorP1Maquina<4){ //si solo es tocado
                                                    tableroAtaque1[fila][columna]=ANSI_YELLOW+"TT"+ANSI_RESET;
                                                }
                                            }
                                            if(tableroJugador2[fila][columna] == "S1" || tableroJugador2[fila][columna] == "S2"){
                                                System.out.println("Lanzamiento del jugador: "+ANSI_YELLOW+"¡SUBMARINO TOCADO!"+ANSI_RESET);
                                                if(tableroJugador2[fila][columna] == "S1"){
                                                    contadorS1Maquina++;    
                                                }else if(tableroJugador2[fila][columna] == "S2"){
                                                    contadorS2Maquina++;    
                                                }
                                                if(contadorS1Maquina == 3){
                                                    System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡SUBMARINO HUNDIDO!"+ANSI_RESET);
                                                    for (int i = 0; i < tableroJugador2.length; i++){
                                                        for (int j = 0; j < tableroJugador2.length; j++) {
                                                            if(tableroJugador2[i][j] == "S1"){
                                                                tableroAtaque1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                            }
                                                        }
                                                    }
                                                }else if (contadorS2Maquina == 3){
                                                    System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡SUBMARINO HUNDIDO!"+ANSI_RESET);
                                                    for (int i = 0; i < tableroJugador2.length; i++){
                                                        for (int j = 0; j < tableroJugador2.length; j++) {
                                                            if(tableroJugador2[i][j] == "S2"){
                                                                tableroAtaque1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                            }
                                                        }
                                                    }
                                                }else{
                                                    tableroAtaque1[fila][columna]=ANSI_YELLOW+"TT"+ANSI_RESET;
                                                }
                                            }
                                            if(tableroJugador2[fila][columna]== "F1" || tableroJugador2[fila][columna]== "F2" || tableroJugador2[fila][columna]== "F3"){
                                                System.out.println("Lanzamiento del jugador: "+ANSI_YELLOW+"¡FRAGATA TOCADA!"+ANSI_RESET);
                                                if(tableroJugador2[fila][columna] == "F1"){
                                                    contadorF1Maquina++;
                                                }else if(tableroJugador2[fila][columna] == "F2"){
                                                    contadorF2Maquina++;    
                                                }else if (tableroJugador2[fila][columna] == "F3"){
                                                    contadorF2Maquina++;
                                                }
                                                if(contadorF1Maquina == 2){
                                                    System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡FRAGATA HUNDIDA!"+ANSI_RESET);
                                                    for (int i = 0; i < tableroJugador2.length; i++){
                                                        for (int j = 0; j < tableroJugador2.length; j++) {
                                                            if(tableroJugador2[i][j]=="F1"){
                                                                tableroAtaque1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                            }
                                                        }
                                                    }
                                                }else if(contadorF2Maquina == 2){
                                                    System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡FRAGATA HUNDIDA!"+ANSI_RESET);
                                                    for (int i = 0; i < tableroJugador2.length; i++){
                                                        for (int j = 0; j < tableroJugador2.length; j++) {
                                                            if(tableroJugador2[i][j] == "F2"){
                                                                tableroAtaque1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                            }
                                                        }
                                                    }
                                                }else if(contadorF3Maquina == 2){
                                                    System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡FRAGATA HUNDIDA!"+ANSI_RESET);
                                                    for (int i = 0; i < tableroJugador2.length; i++){
                                                        for (int j = 0; j < tableroJugador2.length; j++) {
                                                            if(tableroJugador2[i][j]=="F3"){
                                                                tableroAtaque1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                            }
                                                        }
                                                    }
                                                }else{
                                                    tableroAtaque1[fila][columna]=ANSI_YELLOW+"TT"+ANSI_RESET;
                                                }
                                            }
                                            else if(tableroJugador2[fila][columna]== "L1" || tableroJugador2[fila][columna]== "L2" || tableroJugador2[fila][columna]== "L3" || tableroJugador2[fila][columna]== "4"){//para las lanchas
                                                System.out.println("Lanzamiento del jugador: "+ANSI_RED+"¡LANCHA HUNDIDA!"+ANSI_RESET);
                                                tableroAtaque1[fila][columna]=ANSI_RED+"HH"+ANSI_RESET;
                                            }
                                            contadorTocadosJugador++;
                                        }else{ //si no hay ningun barco
                                            System.out.println("Lanzamiento del jugador: "+ANSI_BLUE+"¡AGUA!"+ANSI_RESET);
                                            tableroAtaque1[fila][columna]=ANSI_BLUE+"AA"+ANSI_RESET;
                                        }
                                        //limpiarPantalla();
                                        if(contadorTocadosJugador == 20){
                                            ganador=true;
                                            System.out.println("Eres el ganador!");
                                        }
                                        break;
                                    }
                                    case 2:{
                                        //guardar
                                        break;
                                    }
                                    case 3:{ //guardar y salir

                                        break;
                                    }
                                    case 4:{ //salir
                                        ganador=true;
                                        break;
                                    }
                                } 
                                turno++;
                            }else{ //turno de la máquina
                                System.out.println("\n" + "Turno de la máquina.");
                                int fila = aleatorio.nextInt(10)+1;
                                int columna = aleatorio.nextInt(10)+1;
                                if(tableroJugador1[fila][columna]!="  "){
                                    if(tableroJugador1[fila][columna]=="P1"){
                                        System.out.println("Lanzamiento de la máquina: "+ANSI_YELLOW+"¡PORTAAVION TOCADO!"+ANSI_RESET);
                                        contadorP1Jugador++;
                                        if(contadorP1Jugador==4){
                                            for (int i = 0; i < tableroJugador1.length; i++){
                                                for (int j = 0; j < tableroJugador1.length; j++) {
                                                    if(tableroJugador1[i][j]=="P1"){
                                                        tableroJugador1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                    }
                                                }
                                            }
                                        }else{
                                            tableroJugador1[fila][columna]=ANSI_YELLOW+"TT"+ANSI_RESET;
                                        }
                                    }
                                    if(tableroJugador1[fila][columna]== "S1" || tableroJugador1[fila][columna]== "S2"){
                                        System.out.println("Lanzamiento de la máquina: "+ANSI_YELLOW+"¡SUBMARINO TOCADO!"+ANSI_RESET);
                                        if(tableroJugador1[fila][columna]== "S1"){
                                            contadorS1Jugador++;
                                            if(contadorS1Jugador==3){
                                                System.out.println("Lanzamiento de la máquina: "+ANSI_RED+"¡SUBMARINO HUNDIDO!"+ANSI_RESET);
                                                for (int i = 0; i < tableroJugador1.length; i++){
                                                    for (int j = 0; j < tableroJugador1.length; j++) {
                                                        if(tableroJugador1[i][j]=="S1"){
                                                            tableroJugador1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                        }
                                                    }
                                                }
                                            }
                                        }else if(tableroJugador1[fila][columna]== "S2"){
                                            contadorS2Jugador++;
                                            if(contadorS2Jugador==3){
                                                System.out.println("Lanzamiento de la máquina: "+ANSI_RED+"¡SUBMARINO HUNDIDO!"+ANSI_RESET);
                                                for (int i = 0; i < tableroJugador1.length; i++){
                                                    for (int j = 0; j < tableroJugador1.length; j++) {
                                                        if(tableroJugador1[i][j]=="S2"){
                                                            tableroJugador1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                        }
                                                    }
                                                }
                                            }
                                        }else{
                                            tableroJugador1[fila][columna]=ANSI_YELLOW+"TT"+ANSI_RESET;
                                        }
                                    }
                                    if(tableroJugador1[fila][columna]== "F1" || tableroJugador1[fila][columna]== "F2" || tableroJugador1[fila][columna]== "F3"){
                                        System.out.println("Lanzamiento de la máquina: "+ANSI_YELLOW+"¡FRAGATA TOCADA!"+ANSI_RESET);
                                        if(tableroJugador1[fila][columna]== "F1"){
                                            contadorF1Jugador++;
                                            if(contadorF1Jugador==2){
                                                System.out.println("Lanzamiento de la máquina: "+ANSI_RED+"¡FRAGATA HUNDIDA!"+ANSI_RESET);
                                                for (int i = 0; i < tableroJugador1.length; i++){
                                                    for (int j = 0; j < tableroJugador1.length; j++) {
                                                        if(tableroJugador1[i][j]=="F1"){
                                                            tableroJugador1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                        }
                                                    }
                                                }
                                            }
                                        }else if(tableroJugador1[fila][columna]== "F2"){
                                            contadorF2Jugador++;
                                            if(contadorF2Jugador==2){
                                                System.out.println("Lanzamiento de la máquina: "+ANSI_RED+"¡FRAGATA HUNDIDA!"+ANSI_RESET);
                                                for (int i = 0; i < tableroJugador1.length; i++){
                                                    for (int j = 0; j < tableroJugador1.length; j++) {
                                                        if(tableroJugador1[i][j]=="F2"){
                                                            tableroJugador1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                        }
                                                    }
                                                }
                                            }
                                        }else if(tableroJugador1[fila][columna]== "F3"){
                                            contadorF3Jugador++;
                                            if(contadorF3Jugador==2){
                                                System.out.println("Lanzamiento de la máquina: "+ANSI_RED+"¡FRAGATA HUNDIDA!"+ANSI_RESET);
                                                for (int i = 0; i < tableroJugador1.length; i++){
                                                    for (int j = 0; j < tableroJugador1.length; j++) {
                                                        if(tableroJugador1[i][j]=="F3"){
                                                            tableroJugador1[i][j]=ANSI_RED+"HH"+ANSI_RESET;
                                                        }
                                                    }
                                                }
                                            }
                                        }else{
                                            tableroJugador1[fila][columna]=ANSI_YELLOW+"TT"+ANSI_RESET;
                                        }
                                    }
                                    else if(tableroJugador1[fila][columna]== "L1" || tableroJugador2[fila][columna]== "L2" || tableroJugador2[fila][columna]== "L3" || tableroJugador2[fila][columna]== "4"){//para las lanchas
                                        System.out.println("Lanzamiento de la máquina: "+ANSI_RED+"¡LANCHA HUNDIDA!"+ANSI_RESET);
                                        tableroJugador1[fila][columna]=ANSI_RED+"HH"+ANSI_RESET;
                                    }
                                    contadorTocadosMaquina++;
                                }else{ //si no hay ningun barco
                                    System.out.println("Lanzamiento de la máquina: "+ANSI_BLUE+"¡AGUA!"+ANSI_RESET);
                                    tableroJugador1[fila][columna]=ANSI_BLUE+"AA"+ANSI_RESET;
                                }
                                if(contadorTocadosMaquina == 20){
                                    ganador=true;
                                    System.out.println("Ha ganado la máquina.");
                                }
                                turno++;
                            }
                        }   
                        break;  
                    }
                    case 2:{
                        System.out.println("Has seleccionado cargar partida.");
                        
                        break;
                    }
                    case 3:{
                        break;
                    }   
                }
                break;
            }
            case 2:{ //ayuda
                limpiarPantalla();
                System.out.println("Este es el menú de ayuda. Elige una opción valida.");
                break;
            }
            case 3:{ //salir
                break;
            } 
        }
    } 
}
