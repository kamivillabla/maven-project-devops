# TaskMaster

**TaskMaster** es una aplicación de consola escrita en **Java 21**, enfocada en prácticas modernas de **DevOps**: Testing automatizado y análisis de cobertura.

## Estructura de carpetas

```
taskmaster/
├── src/
│   └── main/java/com/equipo/taskmaster/
│       └── App.java
├── src/test/java/com/equipo/taskmaster/
│   └── AppTest.java
├── pom.xml
└── .github/workflows/ci.yml
```

## Automatización con Maven

Este proyecto utiliza el ciclo de vida estándar de Maven para compilar, testear y generar reportes automáticamente:

```bash
mvn clean package   # Compila y empaqueta el proyecto
mvn test            # Ejecuta los tests
mvn jacoco:report   # Genera reporte de cobertura en HTML
```

---

## CI/CD con GitHub Actions

Cada push o pull request hacia `main` o `develop` dispara automáticamente:

- Compilación y ejecución de tests
- Generación de cobertura con **JaCoCo**
- Upload del reporte HTML como artefacto (`coverage-report`)
- Bloqueo de merges en `main` si los tests fallan

Ruta del workflow:
```
.github/workflows/ci.yml
```

---

## Política de ramas

| Rama     | Protecciones activas                                     |
|----------|-----------------------------------------------------------|
| `main`   | Requiere PR + Tests exitosos + No push directo     |
| `develop`| Tests automáticos vía CI + Sin protecciones extras   |

---

## Cobertura de código

Después de cada ejecución de CI, se genera un reporte HTML accesible como artefacto:

```
target/site/jacoco/index.html
```

> En GitHub: `Actions > Último build > Artifacts > coverage-report`

## Test de ejemplo

El proyecto incluye un test simple para validar que se agrega una tarea correctamente:

```java
@Test
public void testAddTask() {
    App.tasks.clear();
    App.addTask("Terminar ejercicio Maven");
    assertEquals(1, App.tasks.size());
}
```

## Compilar localmente

```bash
git clone https://github.com/kamivillabla/maven-project-devops.git
cd taskmaster
mvn clean package
mvn exec:java o mvn exec:java -Pdev -Denv.name=Dev
```

## Requisitos previos

- JDK 21
- Maven
