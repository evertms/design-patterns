# Patrón de diseño Builder
## Tipo de patrón: creacional
Este patrón es útil si tenemos una clase con un constructor con muchos parámetros. En lo que nos ayuda es que es como tener un constructor "paso a paso". En el ejemplo que se me dio en la entrevista, suponíamos el caso de la creación de un Vehículo que podía ser de dos puertas, cuatro puertas o no tener puertas; tener cuatro ruedas o dos ruedas; tener dos asientos, cuatro asientos, cinco asientos; etc. En lugar de tener un constructor de este estilo:
```
Vehiculo(numPuertas, numAsientos, numRuedas)
```
Lo que nos indica el patrón de diseño Builder es que podemos ir añadiendo partes poco a poco en lugar de hacerlo de la manera de arriba. Obviamente este ejemplo es académico, seguramente en la vida profesional sea un constructor con muchísimos más parámetros. Pero en resumen, este patrón de diseño es útil para:
- Crear objetos complejos paso a paso.
- Separar la construcción del objeto de su representación final, lo que hace el código más legible y fácil de mantener. Si queremos agregar más partes, en vez de modificar el constructor, creamos otro método para agregar tal configuración.
- Cuando un objeto tiene muchas partes o "configuraciones" posibles.
### Diagrama
![[Patrón Builder 1.png]]

### Pseudocódigo
```
class Director
	func make_sports_car(builder)
		builder.reset()
		builder.set_seats(2)
		builder.set_doors(2)
		builder.set_tires(4)
		
	func make_taxi(builder) 
		builder.reset()
		builder.set_seats(4)
		builder.set_seats(4)
		builder.set_tires(4)
		
interface ICarBuilder
	func reset()
	func set_seats(n: int)
	func set_doors(n: int)
	func set_tires(n: int)
	
class SedanBuilder implements ICarBuilder
	private sedan: Sedan
	
	SedanBuilder(_sedan)
		sedan = _sedan
		
	func reset()
        sedan = new Sedan()
        
    func set_seats(n: int)
        sedan.seats = n
        
    func set_doors(n: int)
        sedan.doors = n
        
    func set_tires(n: int)
        sedan.tires = n
        
    func get_result() -> Sedan
        return sedan
        
class Sedan:
    public seats: int
    public doors: int
    public tires: int
    
class CoupeBuilder implements ICarBuilder
	private coupe: Coupe
	
	CoupeBuilder(_coupe)
		coupe = _coupe
		
	func reset()
        coupe = new Coupe()
        
    func set_seats(n: int)
        coupe.seats = n
        
    func set_doors(n: int)
        coupe.doors = n
        
    func set_tires(n: int)
        coupe.tires = n
        
    func get_result() -> Coupe
        return coupe
        
class Coupe: #Aquí tanto Sedan como Coupe pueden heredar de Car
    public seats: int
    public doors: int
    public tires: int

func main()
    sedan_builder = new SedanBuilder()
	coupe_builder = new CoupeBuilder()
	
    director = new Director()
    
    director.make_sports_car(coupe_builder)
    sports_car = coupe_builder.get_result()
    print(sports_car)  # Salida: Sedan con 2 asientos, 2 puertas y 4 neumáticos
    
    director.make_taxi()
    taxi = sedan_builder.get_result()
    print(taxi)  # Salida: Sedan con 4 asientos, 4 puertas y 4 neumáticos
    
```
### Patrones relacionados
- **Abstract Factory.** Por ser patrones creacionales
- **Factory Method.** Por ser patrones creacionales
- **Chain of responsibility.** Ambos manejan objetos con procesos paso a paso
- **Facade.** Ambos simplifican procesos complejos.

### Bibliografía
Refactoring.Guru (2025) *Builder.* refactoring.guru. Recuperado de *https://refactoring.guru/design-patterns/builder/*
DevExpert (2022) *Builder - Patrones de diseño*. devexpert.io. Recuperado de *https://devexpert.io/builder-patrones-diseno/*

### Videos de referencia
https://youtu.be/oP76NM4qZhw?si=uX_1JhQZu0qJ2j5K
https://www.youtube.com/watch?v=Wqx4N4tV_tc