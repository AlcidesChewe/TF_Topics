![UPC LOGO](https://www.canvia.com/wp-content/uploads/2023/08/crymibfuwaapssb.png)

# Tópicos en Ciencias de la Computación - TRABAJO FINAL

## Información del Curso
**Profesor:** Luis Martin, Canaval Sanchez  
**Sección:** CC82  
**Fecha:** JUNIO 2024

## Integrantes
- Charapaqui Reluz, Rommel Alcides - U202021294
- Barrionuevo Gutierrez, Daniel Ulises - U201922128
- Castilla Ochoa, Carlos Alonso - U202116277

# Informe del Proyecto: Simulación de Batalla Pokémon

---

## Introducción

**Problema:**
El proyecto aborda la creación de una simulación de batalla entre Pokémon. El objetivo es modelar una serie de batallas entre criaturas virtuales, cada una con un tipo elemental, para determinar cuál es la más fuerte mediante un sistema de ventajas y desventajas basado en los tipos.

**Solución Propuesta:**
Se ha desarrollado una aplicación en Python que simula batallas entre Pokémon. Cada Pokémon tiene un tipo elemental que afecta su probabilidad de ganar contra otros Pokémon. El programa selecciona dos Pokémon aleatoriamente, determina el ganador basándose en las ventajas de tipo, y sigue este proceso hasta que solo queda un Pokémon vencedor.

![MAPA_MENTAL](https://cdn.discordapp.com/attachments/1224860730852114582/1256508727369138209/image.png?ex=66810671&is=667fb4f1&hm=8e184c1c0cab11e3c352ff1fd0e9973cd3ca12a8d2d4b8f5363f80ca18faa8a4&)

---

## Objetivos

1. **Modelar la estructura básica de un Pokémon**: Crear una clase que represente a un Pokémon con atributos como nombre, tipo y número de victorias.
2. **Implementar el sistema de batalla**: Crear una función que simule una batalla entre dos Pokémon considerando sus tipos.
3. **Simular un torneo**: Desarrollar una función que simule una serie de batallas entre múltiples Pokémon hasta determinar un ganador.
4. **Evaluar el rendimiento**: Analizar los resultados de las batallas para determinar la efectividad y precisión del sistema.

---

## Desarrollo

**Componentes del Problema:**

1. **Clase Pokémon:**
   - **Atributos:** nombre, tipo y número de victorias.
   - **Métodos:** 
     - `__init__`: Inicializa los atributos del Pokémon.
     - `__str__`: Retorna una representación en cadena del Pokémon.
     - `add_win`: Incrementa el contador de victorias del Pokémon.

    ```python
    class Pokemon:
        def __init__(self, name, type_):
            self.name = name
            self.type = type_
            self.wins = 0

        def __str__(self):
            return f"{self.name} [{self.type}]"

        def add_win(self):
            self.wins += 1
    ```

2. **Función de Batalla:**
   - **Ventaja de Tipos:** Un diccionario que define las probabilidades de victoria entre los diferentes tipos de Pokémon.
   - **Lógica de Batalla:** Calcula la probabilidad de victoria de cada Pokémon y determina el ganador basado en un valor aleatorio.

    ```python
    def battle(pokemon1, pokemon2):
        ventaja = {
            "fuego": {"fuego": 0.5, "agua": 0.2, "planta": 0.8, "eléctrico": 0.5, "tierra": 0.5, "roca": 0.2, "volador": 0.8, "fantasma": 0.5, "psiquico": 0.2, "lucha": 0.5, "normal": 0.5},
            "agua": {"fuego": 0.8, "agua": 0.5, "planta": 0.2, "eléctrico": 0.5, "tierra": 0.8, "roca": 0.8, "volador": 0.5, "fantasma": 0.5, "psiquico": 0.2, "lucha": 0.5, "normal": 0.5},
            "planta": {"fuego": 0.2, "agua": 0.8, "planta": 0.5, "eléctrico": 0.5, "tierra": 0.8, "roca": 0.8, "volador": 0.5, "fantasma": 0.5, "psiquico": 0.2, "lucha": 0.5, "normal": 0.5},
            "eléctrico": {"fuego": 0.5, "agua": 0.5, "planta": 0.5, "eléctrico": 0.5, "tierra": 0.8, "roca": 0.2, "volador": 0.5, "fantasma": 0.5, "psiquico": 0.5, "lucha": 0.5, "normal": 0.5},
            "tierra": {"fuego": 0.5, "agua": 0.2, "planta": 0.2, "eléctrico": 0.8, "tierra": 0.5, "roca": 0.8, "volador": 0.2, "fantasma": 0.5, "psiquico": 0.5, "lucha": 0.5, "normal": 0.5},
            "roca": {"fuego": 0.8, "agua": 0.5, "planta": 0.5, "eléctrico": 0.8, "tierra": 0.5, "roca": 0.5, "volador": 0.8, "fantasma": 0.5, "psiquico": 0.5, "lucha": 0.5, "normal": 0.5},
            "volador": {"fuego": 0.2, "agua": 0.8, "planta": 0.8, "eléctrico": 0.5, "tierra": 0.8, "roca": 0.2, "volador": 0.5, "fantasma": 0.5, "psiquico": 0.5, "lucha": 0.5, "normal": 0.5},
            "fantasma": {"fuego": 0.5, "agua": 0.5, "planta": 0.5, "eléctrico": 0.5, "tierra": 0.5, "roca": 0.5, "volador": 0.5, "fantasma": 0.5, "psiquico": 0.8, "lucha": 0.2, "normal": 0.2},
            "psiquico": {"fuego": 0.8, "agua": 0.8, "planta": 0.8, "eléctrico": 0.5, "tierra": 0.5, "roca": 0.5, "volador": 0.5, "fantasma": 0.2, "psiquico": 0.5, "lucha": 0.2, "normal": 0.2},
            "lucha": {"fuego": 0.5, "agua": 0.5, "planta": 0.5, "eléctrico": 0.5, "tierra": 0.5, "roca": 0.5, "volador": 0.8, "fantasma": 0.8, "psiquico": 0.8, "lucha": 0.5, "normal": 0.5},
            "normal": {"fuego": 0.5, "agua": 0.5, "planta": 0.5, "eléctrico": 0.5, "tierra": 0.5, "roca": 0.5, "volador": 0.5, "fantasma": 0.5, "psiquico": 0.5, "lucha": 0.5, "normal": 0.5}
        }

        prob_poke1_gana = ventaja[pokemon1.type][pokemon2.type]
        prob_poke2_wins = 1 - prob_poke1_gana

        winner = pokemon1 if random.random() < prob_poke1_gana else pokemon2
        return winner
    ```

3. **Generación de Pokémon:**
   - Una función que crea una lista de Pokémon con tipos aleatorios.

    ```python
    def crear_poke(n):
        tipos = ["fuego", "agua", "planta", "eléctrico", "tierra", "roca", "volador", "fantasma", "psíquico", "lucha", "normal"]
        pokemons = []
        for i in range(n):
            name = f"Poke{i+1}"
            tipo = random.choice(tipos)
            pokemons.append(Pokemon(name, tipo))
        return pokemons
    ```

4. **Simulación del Torneo:**
   - Selecciona dos Pokémon aleatoriamente para cada batalla.
   - Actualiza el contador de victorias del ganador.
   - Elimina al Pokémon perdedor de la lista.
   - Repite el proceso hasta que quede un solo Pokémon.

    ```python
    def main():
        pokemons = crear_poke(10)

        print("Lista de pokemones iniciales:")
        for pokemon in pokemons:
            print(pokemon)

        round_num = 1
        all_pokemons = pokemons.copy()

        while len(pokemons) > 1:
            print("\nronda", round_num)
            poke1, poke2 = random.sample(pokemons, 2)
            winner = battle(poke1, poke2)
            winner.add_win()
            loser = poke1 if winner == poke2 else poke2
            print(poke1,"vs",poke2,"=>","gano",winner)
            pokemons.remove(loser)
            round_num += 1

        print(f"\n¡El ganador es {pokemons[0]}!\n")

        print("Resultados finales:")
        for pokemon in all_pokemons:
            print(pokemon, ":",pokemon.wins,"victorias")

    if __name__ == "__main__":
        main()
    ```

---

## Dependencias y Relaciones

- **Dependencia entre Pokémon y Batallas:** La función de batalla depende de la existencia de objetos Pokémon con atributos específicos.
- **Relación entre Tipo y Resultado:** Las probabilidades de victoria están directamente relacionadas con el tipo de cada Pokémon, lo que define la estrategia del juego.
- **Interacción entre Componentes:** La generación de Pokémon, la función de batalla y la simulación del torneo trabajan conjuntamente para producir el resultado final.

---

## Conclusiones

El proyecto logra simular de manera efectiva una serie de batallas entre Pokémon, utilizando un sistema de ventajas y desventajas basado en tipos. La implementación en Python demuestra cómo se pueden modelar y simular dinámicas complejas de juego. Los resultados muestran que el enfoque es robusto y puede ser expandido con características adicionales, como más tipos de Pokémon, habilidades especiales, y estrategias avanzadas.


