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

![MAPA_MENTAL](https://cdn.discordapp.com/attachments/1224860730852114582/1256530950565920789/image.png?ex=66811b23&is=667fc9a3&hm=dc2077a6864d80de11fd6a42b9e132a171dc91bd90c9a98438d7b10cee50cf3b&)

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

**Clase Thing**
```python
class Thing:
    """This represents any physical object that can appear in an Environment."""
    def __repr__(self):
        return '<{}>'.format(getattr(self, '__name__', self.__class__.__name__))
```
**Clase Agent**

```python
Copiar código
class Agent(Thing):
    """An Agent is a subclass of Thing with one required slot, .program."""
    def __init__(self, program=None):
        self.alive = True
        self.bump = False
        self.holding = []
        self.performance = 0
        if program is None or not isinstance(program, collections.abc.Callable):
            def program(percept):
                return eval(input('Percept={}; action? '.format(percept)))
        self.program = program
    def can_grab(self, thing):
        return False
```

**Clase Environment**

```python
Copiar código
class Environment:
    """Abstract class representing an Environment."""
    def __init__(self):
        self.things = []
        self.agents = []
    def percept(self, agent):
        raise NotImplementedError
    def execute_action(self, agent, action):
        raise NotImplementedError
    def step(self):
        if not self.is_done():
            actions = []
            for agent in self.agents:
                if agent.alive:
                    actions.append(agent.program(self.percept(agent)))
                else:
                    actions.append("")
            for (agent, action) in zip(self.agents, actions):
                self.execute_action(agent, action)
            self.exogenous_change()
```

**Dependencias y Relaciones**
### El archivo agents.py depende de varias utilidades definidas en utils.py:

**Funciones de Utilidad en utils.py**

```python
def sequence(iterable):
    return iterable if isinstance(iterable, collections.abc.Sequence) else tuple([iterable])

def remove_all(item, seq):
    if isinstance(seq, str):
        return seq.replace(item, '')
    else:
        return [x for x in seq if x != item]

def euclidean_distance(x, y):
    return np.sqrt(sum((_x - _y) ** 2 for _x, _y in zip(x, y)))
```
Además, se implementan varios tipos de agentes específicos:

**Agente Basado en Modelo**
```python
def ModelBasedReflexAgentProgram(rules, update_state, model):
    def program(percept):
        program.state = update_state(program.state, program.action, percept, model)
        rule = rule_match(program.state, rules)
        action = rule.action
        return action
    program.state = program.action = None
    return program
```
## Impacto de la Solución
La solución propuesta permite la creación y simulación de entornos diversos con relativa facilidad. Los agentes pueden ser evaluados en términos de su rendimiento en diferentes escenarios, lo cual proporciona una base sólida para el desarrollo de sistemas de inteligencia artificial más complejos.

**Simulación del Entorno de Vacío**
```python
class VacuumEnvironment(XYEnvironment):
    def __init__(self, width=10, height=10):
        super().__init__(width, height)
        self.add_walls()
    def percept(self, agent):
        status = 'Dirty' if self.some_things_at(agent.location, Dirt) else 'Clean'
        bump = 'Bump' if agent.bump else 'None'
        return (status, bump)
    def execute_action(self, agent, action):
        agent.bump = False
        if action == 'Suck':
            dirt_list = self.list_things_at(agent.location, Dirt)
            if dirt_list:
                agent.performance += 100
                self.delete_thing(dirt_list[0])
        else:
            super().execute_action(agent, action)
        if action != 'NoOp':
            agent.performance -= 1
```
## Simulación Pokemon
![Simuñación1](https://cdn.discordapp.com/attachments/1224860730852114582/1256538289456943114/image.png?ex=668121f9&is=667fd079&hm=b68f916a8569f8732fc8e4b7926d5244f1fda41cafc54d740d857627bd3f04ea&)
![Simulación2](https://cdn.discordapp.com/attachments/1224860730852114582/1256538338240757813/image.png?ex=66812205&is=667fd085&hm=33f177c0ee7b384940be509981193564dc43d52d9ba3996e9b5248568bf43e71&)

# Conclusiones
El proyecto ha demostrado ser una herramienta valiosa para la creación y simulación de agentes inteligentes en diversos entornos. La arquitectura modular permite una fácil extensión y adaptación a nuevos escenarios. El enfoque basado en agentes reflexivos y basados en modelos proporciona una comprensión profunda de las técnicas de inteligencia artificial y sus aplicaciones prácticas.

Este marco puede ser utilizado como base para investigaciones futuras y para el desarrollo de aplicaciones más avanzadas en el campo de la inteligencia artificial.
