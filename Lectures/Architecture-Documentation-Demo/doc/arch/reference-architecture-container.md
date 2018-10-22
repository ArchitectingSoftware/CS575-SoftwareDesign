# Blockchain Reference Architecture

## Architecture Overview

The purpose of this project is explore the inter-workings of how a block chain and consensus algorithms work to demonstrate modern architecture and design concepts.  

## Architecture Diagram

```plantuml
@startuml "BC-Architecture-Container"
!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Container.puml

LAYOUT_TOP_DOWN
'LAYOUT_AS_SKETCH
'LAYOUT_WITH_LEGEND

Person(admin, "User")
package "Container Runtime" <<boundary>> as c1 {
    package "Blockchain Simulator" <<boundary>> as c2 {
        hide stereotype

        Container(wa, "WebApp", "Angular", "Allows users to understand basic Blockchain Operators")

        Container(wa_miner, "Embedded Miner", "Typescript", "Uses Observables in the client to mine blocks")

        Container(wa_cli, "Miner Client", "Typescript", "Uses Observables in the client to mine blocks")

        Container(go_miner, "GoLang Miner", "GoLang", "Uses GinGonic framework [[https://gin-gonic.github.io/gin/ link]]")

        Container(kotlin_miner, "Kotlin Miner", "Kotlin", "Uses Kotlin co-routines and the KTOR framework")

        Container(node_miner, "Node Miner", "Typescript", "Uses Koa's async await functionality - built on top of generators")

        Container(scala_miner, "Scala Miner", "Scala", "Uses akka/HTTP")

        Rel_L(wa, wa_miner,"typescript angular service")
        Rel_R(wa, wa_cli,"typescript angular service")

        Rel(wa_cli,go_miner,"HTTP")
        Rel(wa_cli,kotlin_miner,"HTTP")
        Rel(wa_cli,node_miner,"HTTP")
        Rel(wa_cli,scala_miner,"HTTP")
    }
}

Rel(admin, wa, "Uses", "HTTPS")
@enduml
```

## Architecture Components

| Component | Description |
| --------- | ----------- |
| Web App   |  The web application uses the Angular 6 framework and a number of best practices for state management and asynchronous integration with web services.  The Web App is deployed in a container using the Ngenix web server. |
| Miner Client | The Miner client is a library in the main web app that handles routing to a minor implementation, either internal or external via a web service |
| Embedded Minor | This is a typescript implementation embedded in the web client codebase. It uses observables to iterate the calculations versus a long running loop to respect the single threaded model of the browser.  |
| GoLang Miner | A high performance miner written in the go programming language. Concurrency is handled via Go's novel concurrency model - specifically `goroutines` |
|Kotlin Miner | Kotlin is a modern JVM language, one of its unique concurrency and high-performance computing capabilites are based on coroutines.  The Kotlin Miner uses the [ktor](https://ktor.io) framework


