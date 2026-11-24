
# Diagrama de clases simplificado — SolitarioPiramide-Modelo

```mermaid
%%{init: {
    "theme": "base",
    "themeVariables": {
        "darkMode": true,
        "fontFamily": "Arial",
        "fontSize": "28px",
        "background": "#0D1117",
        "primaryColor": "#FFFFFF",
        "primaryTextColor": "#000000",
        "primaryBorderColor": "#FFFFFF",
        "secondaryColor": "#0D1117",
        "secondaryTextColor": "#FFFFFF",
        "tertiaryColor": "#0D1117",
        "tertiaryTextColor": "#FFFFFF",
        "lineColor": "#FFFFFF",
        "textColor": "#FFFFFF",
        "classText": "#000000",
        "edgeLabelBackground": "#0D1117"
    },
    "themeCSS": ".relation { stroke: #FFFFFF !important; stroke-width: 2.5px !important; } .edgeLabel rect, .labelBkg { fill: #0D1117 !important; opacity: 1 !important; } .edgeLabel, .edgeLabel span, .edgeLabel p, .edgeLabel div { background-color: #0D1117 !important; color: #FFFFFF !important; } .edgeLabel text, .relationLabel text, .cardinality text, .edgeTerminals text { fill: #FFFFFF !important; font-size: 28px !important; } marker path { stroke: #FFFFFF !important; } .classTitle { font-weight: bold !important; }",
    "class": {
        "hideEmptyMembersBox": true
    }
}}%%

classDiagram
    direction TB

    %% Clases principales
    class JuegoSolitario
    class Carta
    class Mazo
    class Piramide
    class Pozo
    class TiempoDeJuego
    class ReglasDePuntaje
    class RegistroDeRecords
    class MovimientoInvalido

    class Error {
        <<Pharo Kernel>>
    }

    %% Jerarquia de ubicaciones
    class UbicacionCarta {
        <<abstract>>
    }

    class UbicacionPiramide
    class UbicacionPozo

    %% Jerarquia de estados
    class EstadoPartida {
        <<abstract>>
    }

    class EnCurso
    class Ganada
    class Perdida

    %% Jerarquia de movimientos
    class Movimiento {
        <<abstract>>
    }

    class EliminarRey
    class EliminarPar
    class RobarCarta
    class ReciclarPozo

    %% Herencias
    Error <|-- MovimientoInvalido

    UbicacionCarta <|-- UbicacionPiramide
    UbicacionCarta <|-- UbicacionPozo

    EstadoPartida <|-- EnCurso
    EstadoPartida <|-- Ganada
    EstadoPartida <|-- Perdida

    Movimiento <|-- EliminarRey
    Movimiento <|-- EliminarPar
    Movimiento <|-- RobarCarta
    Movimiento <|-- ReciclarPozo

    %% Composiciones y asociaciones principales
    JuegoSolitario *-- "1" Mazo : mazo
    JuegoSolitario *-- "1" Piramide : piramide
    JuegoSolitario *-- "1" Pozo : pozo
    JuegoSolitario *-- "1" TiempoDeJuego : tiempo
    JuegoSolitario *-- "1" EstadoPartida : estado
    JuegoSolitario *-- "0..*" Movimiento : historial
    JuegoSolitario --> "1" RegistroDeRecords : registroDeRecords
    JuegoSolitario ..> ReglasDePuntaje : consulta
    JuegoSolitario ..> MovimientoInvalido : señala

    %% Relaciones de las cartas
    Mazo o-- "0..52" Carta : cartas
    Piramide o-- "0..28" Carta : cartas
    Pozo --> "1" Mazo : reserva
    Pozo o-- "0..24" Carta : descarte

    %% Relaciones de los movimientos
    EliminarRey --> "1" UbicacionCarta : ubicacion
    EliminarPar --> "2" UbicacionCarta : ubicacionA / ubicacionB

    EliminarRey ..> ReglasDePuntaje : consulta
    EliminarPar ..> ReglasDePuntaje : consulta

    EliminarRey ..> MovimientoInvalido : señala
    EliminarPar ..> MovimientoInvalido : señala
    RobarCarta ..> MovimientoInvalido : señala
    ReciclarPozo ..> MovimientoInvalido : señala
    EstadoPartida ..> MovimientoInvalido : señala

    %% Estilos
    classDef blanca fill:#FFFFFF,stroke:#FFFFFF,stroke-width:2px,color:#000000,font-weight:bold

    cssClass "JuegoSolitario" blanca
    cssClass "Carta" blanca
    cssClass "Mazo" blanca
    cssClass "Piramide" blanca
    cssClass "Pozo" blanca
    cssClass "TiempoDeJuego" blanca
    cssClass "ReglasDePuntaje" blanca
    cssClass "RegistroDeRecords" blanca
    cssClass "EstadoPartida" blanca
    cssClass "EnCurso" blanca
    cssClass "Ganada" blanca
    cssClass "Perdida" blanca
    cssClass "Movimiento" blanca
    cssClass "EliminarRey" blanca
    cssClass "EliminarPar" blanca
    cssClass "RobarCarta" blanca
    cssClass "ReciclarPozo" blanca
    cssClass "UbicacionCarta" blanca
    cssClass "UbicacionPiramide" blanca
    cssClass "UbicacionPozo" blanca
    cssClass "Error" blanca
    cssClass "MovimientoInvalido" blanca
```
