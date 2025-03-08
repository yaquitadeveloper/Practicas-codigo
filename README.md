```mermaid
stateDiagram-v2
    [*] --> Inicio
    
    state Inicio {
        [*] --> SeleccionNivelDificultad
        SeleccionNivelDificultad --> SeleccionTemática: Nivel Seleccionado
        SeleccionTemática --> PreparaciónTablero: Temática Seleccionada
    }
    
    state Jugando {
        [*] --> EsperandoMovimiento
        EsperandoMovimiento --> VolteandoPrimeraCarta: Carta Seleccionada
        VolteandoPrimeraCarta --> EsperandoSegundaCarta: Primera Carta Volteada
        EsperandoSegundaCarta --> ComparandoCartas: Segunda Carta Seleccionada
        
        state ComparandoCartas {
            [*] --> VerificarCoincidencia
            VerificarCoincidencia --> ActualizarContadorParejas: Coinciden
            VerificarCoincidencia --> VoltearCartas: No Coinciden
            
            ActualizarContadorParejas --> VerificarVictoriaTotal
            VerificarVictoriaTotal --> EsperandoMovimiento: Parejas < Total
            VerificarVictoriaTotal --> [*]: ¡Victoria!
            
            VoltearCartas --> EsperandoMovimiento
        }
        
        ComparandoCartas --> VerificarTiempoRestante
        VerificarTiempoRestante --> EsperandoMovimiento: Tiempo > 0
        VerificarTiempoRestante --> FinalizarPorTiempo: Tiempo = 0
    }
    
    FinalizarPorTiempo --> MostrarResultadoParcial
    MostrarResultadoParcial --> VolverAlInicio
    
    Jugando --> MostrarVictoriaSimple: Todas las Parejas Encontradas
    MostrarVictoriaSimple --> VolverAlInicio
    
    Inicio --> Jugando: Tablero Listo
    Jugando --> [*]: Salir
