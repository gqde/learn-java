# RUTA COMPLETA PARA DOMINAR JAVA DE CERO A SENIOR

---

## STACK DE INSTALACIÓN EN LINUX UBUNTU

```bash
# ============================================
# 1. ACTUALIZAR EL SISTEMA
# ============================================
sudo apt update && sudo apt upgrade -y

# ============================================
# 2. HERRAMIENTAS ESENCIALES DEL SISTEMA
# ============================================
sudo apt install -y curl wget apt-transport-https software-properties-common \
  gnupg lsb-release ca-certificates build-essential unzip git

# Configurar Git
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"

# ============================================
# 3. OPENJDK 21 (LTS ACTUAL)
# ============================================
sudo apt install -y openjdk-21-jdk

# Verificar instalación
java --version
javac --version

# Configurar JAVA_HOME
echo 'export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Verificar JAVA_HOME
echo $JAVA_HOME
java -version

# ============================================
# 4. MAVEN (GESTOR DE DEPENDENCIAS Y BUILD)
# ============================================
sudo apt install -y maven

# Verificar
mvn --version

# Configurar settings.xml para repositorio local
mkdir -p ~/.m2
cat > ~/.m2/settings.xml << 'EOF'
<settings>
  <localRepository>${user.home}/.m2/repository</localRepository>
</settings>
EOF

# ============================================
# 5. GRADLE (ALTERNATIVA A MAVEN)
# ============================================
sudo snap install gradle --classic

# Verificar
gradle --version

# ============================================
# 6. INTELLIJ IDEA COMMUNITY EDITION (IDE)
# ============================================
sudo snap install intellij-idea-community --classic

# Alternativa: VS Code con extensiones Java
sudo snap install --classic code
code --install-extension vscjava.vscode-java-pack
code --install-extension vscjava.vscode-java-debug
code --install-extension vscjava.vscode-maven
code --install-extension vscjava.vscode-gradle
code --install-extension vscjava.vscode-spring-boot-dashboard
code --install-extension vmware.vscode-spring-boot
code --install-extension redhat.java
code --install-extension GabrielBB.vscode-lombok

# ============================================
# 7. DOCKER
# ============================================
sudo apt install -y docker.io docker-compose-v2
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
# Cerrar sesión y volver para aplicar el grupo

# ============================================
# 8. POSTGRESQL
# ============================================
sudo apt install -y postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Crear usuario y base de datos de práctica
sudo -u postgres psql -c "CREATE USER devuser WITH PASSWORD 'devpass';"
sudo -u postgres psql -c "CREATE DATABASE devdb OWNER devuser;"
sudo -u postgres psql -c "ALTER USER devuser CREATEDB;"

# ============================================
# 9. MYSQL (ALTERNATIVA)
# ============================================
sudo apt install -y mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql

# ============================================
# 10. SQLITE3
# ============================================
sudo apt install -y sqlite3 libsqlite3-dev

# ============================================
# 11. NODE.JS (ÚTIL PARA FRONTENDS SPA)
# ============================================
sudo snap install node --classic

# ============================================
# 12. HERRAMIENTAS DE BASE DE DATOS (GUI)
# ============================================
sudo snap install dbeaver-ce

# ============================================
# 13. POSTMAN (PRUEBAS DE API)
# ============================================
sudo snap install postman

# ============================================
# 14. HERRAMIENTAS ADICIONALES
# ============================================
sudo apt install -y jq tree httpie

# ============================================
# 15. SDKMAN (GESTOR DE VERSIONES DE JAVA)
# ============================================
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# Instalar versiones adicionales de Java con SDKMAN
# sdk install java 17.0.9-tem
# sdk install java 21.0.2-tem
# sdk list java          # ver todas las distribuciones disponibles

# ============================================
# 16. VERIFICACIÓN FINAL
# ============================================
echo "=== VERIFICACIÓN DEL STACK ==="
echo "java: $(java --version | head -1)"
echo "javac: $(javac --version)"
echo "mvn: $(mvn --version | head -1)"
echo "gradle: $(gradle --version | grep Gradle)"
echo "git: $(git --version)"
echo "docker: $(docker --version)"
echo "psql: $(psql --version)"
echo "=== INSTALACIÓN COMPLETADA ==="
```

---

## VISIÓN GENERAL DE LOS 50 MÓDULOS

| Fase | Módulos | Área |
|---|---|---|
| Fundamentos de Programación | M1 - M8 | Sintaxis, tipos, operadores, control de flujo, métodos, arreglos, strings |
| Programación Orientada a Objetos | M9 - M15 | Clases, encapsulamiento, herencia, polimorfismo, interfaces, clases abstractas, enums |
| Java Intermedio | M16 - M21 | Excepciones, colecciones, genéricos, lambdas, streams, Date/Time |
| Java Avanzado | M22 - M31 | Concurrencia, I/O, serialización, regex, records, sealed classes, reflection, modules, JNI, annotations |
| Plataforma JVM | M32 - M36 | JVM, GC, Maven/Gradle, DI, logging, configuración |
| Acceso a Datos | M37 - M40 | JDBC, JPA/Hibernate básico, JPA/Hibernate avanzado, jOOQ y patrones |
| Desarrollo Web | M41 - M47 | Spring Boot, Spring MVC, REST APIs, Spring Security, WebFlux, WebSocket, testing web |
| Prácticas Profesionales | M48 - M50 | Testing, SOLID/patrones, arquitectura, Docker, CI/CD, cloud |

---

## MÓDULO 1: INTRODUCCIÓN A LA PROGRAMACIÓN Y AL ECOSISTEMA JAVA

**Descripción:** Este módulo sienta las bases absolutas. Aprenderás qué es la programación, cómo funciona un lenguaje compilado y ejecutado en una máquina virtual, la historia y evolución de Java, la arquitectura del ecosistema JVM, y configurarás tu entorno de desarrollo completo en Linux. Al terminar, entenderás cómo un archivo .java se convierte en un programa ejecutable.

1. ¿Qué es programar y qué es un lenguaje de programación
2. Qué es un algoritmo y por qué es la base de todo
3. Pseudocódigo: planificar lógica antes de escribir código
4. Historia de Java: James Gosling y Sun Microsystems (1995)
5. El lema "Write Once, Run Anywhere"
6. Evolución de Java: de 1.0 a Java 21
7. LTS releases: Java 8, 11, 17, 21
8. Diferencia entre lenguajes compilados e interpretados
9. Java como lenguaje híbrido: compilado + interpretado
10. Qué es bytecode (.class files)
11. Qué es la JVM (Java Virtual Machine)
12. El ciclo: .java → javac → .class → JVM → ejecución
13. JDK vs JRE vs JVM: las tres piezas
14. El JDK: Java Development Kit completo
15. El JRE: Java Runtime Environment
16. Diferentes distribuciones de JDK: OpenJDK, Temurin, Corretto, GraalVM
17. Oracle JDK vs OpenJDK: diferencias y licencias
18. Qué es HotSpot JVM
19. JIT (Just-In-Time) compilation en Java
20. AOT (Ahead-Of-Time) compilation con GraalVM Native Image
21. Instalación de OpenJDK 21 en Ubuntu paso a paso
22. Configurar JAVA_HOME
23. Verificar la instalación: java -version, javac -version
24. SDKMAN como gestor de versiones de Java
25. Comando javac: compilar archivos .java
26. Comando java: ejecutar clases compiladas
27. Comando jar: crear archivos .jar
28. Comando javadoc: generar documentación
29. Comando jshell: el REPL interactivo de Java
30. Tu primer Hola Mundo: class y main method
31. La estructura de un archivo .java
32. La clase pública y el nombre del archivo
33. El método main: public static void main(String[] args)
34. System.out.println para imprimir
35. System.out.print sin salto de línea
36. System.err.println para errores
37. System.in para entrada de datos
38. Scanner para leer entrada del usuario
39. Packages en Java: organizar el código
40. La sentencia package
41. La sentencia import
42. Import estático: import static
43. Wildcard imports: import java.util.*
44. El package java.lang: importado automáticamente
45. Convenciones de nombres en Java
46. CamelCase para clases y métodos
47. camelCase para variables locales
48. UPPER_SNAKE_CASE para constantes
49. $ en nombres (reservado para generados por compilador)
50. Palabras reservadas de Java (keywords)
51. Comentarios de una línea (//)
52. Comentarios de múltiples líneas (/* */)
53. Comentarios Javadoc (/** */)
54. Tags Javadoc: @param, @return, @throws
55. Anotaciones básicas: @Override, @Deprecated, @SuppressWarnings
56. Instalación de IntelliJ IDEA Community Edition
57. Configuración inicial de IntelliJ
58. Crear un proyecto en IntelliJ
59. Anatomía de un proyecto Java en IntelliJ
60. Directorio src/main/java y src/test/java
61. Compilar y ejecutar desde IntelliJ
62. Debugging básico en IntelliJ
63. Breakpoints y stepping
64. Variables window y watch expressions
65. Alternativa: VS Code con Java Extension Pack
66. Maven: gestor de dependencias y build (introducción)
67. El archivo pom.xml
68. mvn compile, mvn test, mvn package
69. Gradle como alternativa a Maven
70. El archivo build.gradle
71. Tipos de aplicaciones Java
72. Aplicaciones de consola
73. Aplicaciones de escritorio: Swing y JavaFX
74. Aplicaciones web con Jakarta EE (antiguo Java EE)
75. Aplicaciones web con Spring Boot
76. Aplicaciones móviles: Android (históricamente Java)
77. Microservicios con Spring Boot
78. Java en el ranking de popularidad de lenguajes
79. Casos de uso industriales de Java
80. Empresas y productos que usan Java
81. Comparativa breve: Java vs C#
82. Comparativa breve: Java vs Python
83. Comparativa breve: Java vs Kotlin
84. Comparativa breve: Java vs Go
85. El ecosistema Java: Jakarta EE, Spring, Hibernate
86. Maven Central: el repositorio de paquetes
87. La comunidad Java y recursos de aprendizaje
88. Documentación oficial: docs.oracle.com
89. OpenJDK: proyecto open source
90. Certificaciones de Oracle para Java
91. Decompiladores: JD-GUI, CFR, Procyon
92. El bytecode Java y javap para inspeccionar
93. Git: configuración inicial para proyectos Java
94. .gitignore para proyectos Java/Maven/Gradle
95. Estructura de carpetas estándar de Maven
96. README.md: documentar tu proyecto
97. Patrones de código limpio desde el día uno
98. Java Style Guides: Google Java Style
99. Checkstyle para análisis estático
100. Roadmap de este temario y plan de estudio

---

## MÓDULO 2: VARIABLES, CONSTANTES Y TIPOS DE DATOS

**Descripción:** Este módulo profundiza en el sistema de tipos de Java. Aprenderás a declarar variables, entenderás la diferencia entre tipos primitivos y tipos de referencia, dominarás los 8 tipos primitivos, trabajarás con constantes (final), conversiones de tipo (casting), y el concepto de scope. Java es un lenguaje fuertemente tipado, y entender los tipos es fundamental.

1. ¿Qué es una variable y cómo se almacena en memoria
2. Declaración de variables con tipo explícito
3. Inicialización de variables en la declaración
4. Reglas para nombres válidos de identificadores
5. Convención: camelCase para variables locales
6. Java como lenguaje fuertemente tipado
7. Inference de tipo con var (Java 10+)
8. Reglas de var: solo con inicialización y scope local
9. Lectura de valores con Scanner
10. Escritura con System.out.println
11. Concatenación con el operador +
12. System.out.printf con formato (printf style)
13. Text blocks para strings multilínea (Java 15+)
14. Tipos primitivos enteros: byte (8 bits)
15. Tipos primitivos enteros: short (16 bits)
16. Tipos primitivos enteros: int (32 bits)
17. Tipos primitivos enteros: long (64 bits) y sufijo L
18. Literales enteros: decimal, hexadecimal (0x), binario (0b), octal (0o)
19. Separadores de dígitos: 1_000_000
20. Tipo float (32 bits) y sufijo f
21. Tipo double (64 bits) - el default para decimales
22. Diferencia entre float y double
23. Literal double: 3.14, 3.14d
24. Notación científica: 1.5e10
25. Tipo boolean: true y false
26. Boolean NO es numérico en Java (diferente a C)
27. Tipo char (16 bits) y Unicode
28. Literales char: 'A', '\n', '\u0041'
29. Secuencias de escape: \n, \t, \\, \", \'
30. El wrapper class Integer
31. El wrapper class Double
32. El wrapper class Boolean
33. El wrapper class Character
34. Los 8 wrapper classes: Byte, Short, Integer, Long, Float, Double, Boolean, Character
35. Constantes con final
36. final en variables: no se puede reasignar
37. static final para constantes de clase
38. UPPER_SNAKE_CASE para constantes
39. Constantes del wrapper: Integer.MAX_VALUE, Integer.MIN_VALUE
40. Constantes del wrapper: Double.MAX_VALUE, Double.NaN
41. Tipos de referencia vs tipos primitivos
42. El stack y el heap: dónde se almacenan
43. Tipos primitivos viven en el stack
44. Objetos viven en el heap
45. Las variables de referencia almacenan direcciones
46. null para referencias sin objeto
47. El literal null y NullPointerException
48. Autoboxing: primitivo a wrapper automáticamente
49. Unboxing: wrapper a primitivo automáticamente
50. El rango de cada tipo primitivo
51. Desbordamiento aritmético (overflow) en enteros
52. Overflow silencioso en Java: no hay excepción
53. Underflow en tipos de punto flotante
54. Double.POSITIVE_INFINITY y Double.NEGATIVE_INFINITY
55. Double.NaN y cómo detectarlo con Double.isNaN()
56. Comparación de doubles: evitar ==, usar epsilon
57. Scope de variables: scope de bloque
58. Scope de variables: scope de clase (campos)
59. Scope de variables: scope de método
60. Variables locales: deben inicializarse antes de uso
61. Campos de clase: se inicializan por defecto
62. Valores por defecto: 0, 0.0, false, null
63. Shadowing de variables: campo y parámetro con mismo nombre
64. this para desambiguar
65. Casting implícito (widening): int a long
66. Casting explícito (narrowing): long a int
67. Pérdida de datos en narrowing cast
68. Casting entre primitivos numéricos
69. Casting de char a int y viceversa
70. Casting de String a int: Integer.parseInt()
71. Casting de String a double: Double.parseDouble()
72. Casting de int a String: String.valueOf() o Integer.toString()
73. Integer.valueOf() vs Integer.parseInt()
74. Double.valueOf() vs Double.parseDouble()
75. NumberFormatException en conversiones
76. Manejo seguro con try-catch en conversiones
77. Tuplas: Java no tiene tuplas nativas
78. Pair de Apache Commons o crear record Pair
79. Descartes: Java no tiene underscore para descartes
80. Paso de primitivos por valor (siempre)
81. Paso de referencias por valor (no por referencia)
82. La confusión de "paso por referencia" en Java
83. Strings como tipos de referencia especiales
84. Strings son inmutables en Java
85. == compara referencias, .equals() compara contenido
86. Diferencia entre == y .equals() para Strings
87. String pool: el mecanismo de intern de Strings
88. Tipos anónimos: Java no tiene tipos anónimos como C#
89. Local variable type inference con var (Java 10)
90. var con genéricos: var list = new ArrayList<String>()
91. var en for loops
92. var en try-with-resources
93. var NO funciona en campos de clase, parámetros o retorno
94. Formateo de Strings: String.format()
95. Formateo con System.out.printf()
96. Especificadores: %d, %f, %s, %b, %n
97. DecimalFormat para formato numérico personalizado
98. NumberFormat para formato localizado
99. Locale y formato cultural
100. Resumen: tabla completa de tipos primitivos y wrappers

---

## MÓDULO 3: OPERADORES Y EXPRESIONES

**Descripción:** Dominarás todos los operadores disponibles en Java: aritméticos, lógicos, relacionales, de asignación, bit a bit y otros operadores especiales. Comprenderás la precedencia de operadores, la asociatividad, y cómo se combinan para formar expresiones complejas. También verás el manejo de tipos en expresiones y las conversiones implícitas.

1. ¿Qué es un operador y qué es una expresión?
2. Operador de asignación simple (=)
3. Operadores aritméticos: +, -, *, /
4. Operador de módulo (resto) %
5. Incremento ++ (prefijo y postfijo)
6. Decremento -- (prefijo y postfijo)
7. Diferencia entre i++ y ++i en expresiones
8. Asignación compuesta: +=, -=, *=, /=, %=
9. Precedencia de operadores aritméticos
10. Desbordamiento aritmético (overflow): comportamiento silencioso
11. División entre cero: enteros vs punto flotante
12. ArithmeticException en enteros / 0
13. Division con doubles: Infinity y NaN
14. Operadores de igualdad: == y !=
15. == para primitivos: compara valores
16. == para objetos: compara referencias
17. .equals() para objetos: compara contenido
18. Operadores relacionales: <, >, <=, >=
19. Operadores lógicos: && (AND), || (OR), ! (NOT)
20. Short-circuit evaluation en && y ||
21. Operadores bit a bit: &, |, ^, ~
22. Operadores de desplazamiento: <<, >>, >>>
23. >>> es desplazamiento sin signo (unsigned right shift)
24. Operadores de asignación bit a bit: &=, |=, ^=, <<=, >>=, >>>=
25. Operador ternario condicional (condición ? verdadero : falso)
26. Operador instanceof para verificar tipo
27. Pattern matching for instanceof (Java 16+)
28. Operador new para instanciación
29. Operador . (punto) para acceder a miembros
30. Operador [] para acceder a arreglos
31. Casting con operador () (operador de conversión)
32. Conversiones implícitas en expresiones
33. Promoción de tipos en operaciones mixtas
34. int + double = double (promoción automática)
35. byte + byte = int (promoción automática)
36. Casting necesario para asignar a tipo menor
37. Operaciones con String: concatenación con +
38. Operador + con String y números: conversión automática
39. StringBuilder para concatenación eficiente
40. Comparación de Strings: .equals() vs ==
41. .equalsIgnoreCase() para comparación sin case
42. .compareTo() para comparación lexicográfica
43. Operaciones con boolean: tablas de verdad
44. Operaciones bit a bit con boolean (no aplica directamente)
45. Operaciones con enums usando compareTo()
46. Evaluación de cortocircuito en expresiones complejas
47. Efectos secundarios en expresiones (side effects)
48. Precedencia completa de operadores en Java
49. Tabla de asociatividad (izquierda a derecha vs derecha a izquierda)
50. Uso de paréntesis para alterar la precedencia
51. Expresiones complejas y legibilidad
52. Math.abs(), Math.min(), Math.max()
53. Math.floor(), Math.ceil(), Math.round()
54. Math.pow(), Math.sqrt(), Math.log()
55. Math.sin(), Math.cos(), Math.tan()
56. Math.PI y Math.E
57. Math.random() para números aleatorios (legacy)
58. Random class: new Random()
59. Random.nextInt(), nextDouble(), nextBoolean()
60. Random.nextInt(bound) para rango específico
61. ThreadLocalRandom para concurrencia
62. SecureRandom para criptografía
63. BigDecimal para aritmética de precisión exacta
64. BigDecimal para cálculos financieros
65. BigInteger para números enteros arbitrariamente grandes
66. Operaciones con BigInteger: add, subtract, multiply, divide
67. Operaciones con BigDecimal y escala
68. RoundingMode: HALF_UP, HALF_EVEN, etc.
69. Operaciones con fechas: LocalDate, LocalTime (introducción)
70. Operaciones con Duration y Period (introducción)
71. Expresiones como cuerpo de métodos (no aplica en Java)
72. Java no tiene expression-bodied members como C#
73. Bloques de código estáticos: static { }
74. Bloques de inicialización de instancia: { }
75. Operador ternario como alternativa a if-else
76. Ternarios anidados (posible pero no recomendable)
77. Expresiones con var (Java 10)
78. Expresiones switch (Java 14+): yield keyword
79. Switch expressions con ->
80. Switch expressions con múltiples statements
81. Pattern matching en switch (Java 21)
82. Null handling en switch expressions
83. Operaciones con char: aritmética de caracteres
84. 'A' + 1 = 'B' (aritmética de char)
85. Convertir char a dígito: Character.digit()
86. Convertir dígito a char: (char)('0' + n)
87. Operaciones con booleanos: simplificación de condiciones
88. Leyes de De Morgan simplificadas
89. Evitar condiciones que siempre son true o false
90. Dead code en ramas inalcanzables
91. Expresiones con genéricos y wildcards (introducción)
92. Operaciones con Optional (introducción, Java 8+)
93. Optional.of(), Optional.empty(), Optional.ofNullable()
94. Optional.isPresent(), Optional.isEmpty()
95. Optional.orElse(), Optional.orElseThrow()
96. Operaciones con Streams (introducción, Java 8+)
97. Comparación con Comparator y Comparable (introducción)
98. Comparator.naturalOrder(), Comparator.reverseOrder()
99. Operaciones con Date legacy: java.util.Date (evitar)
100. Resumen: precedencia y mejores prácticas

---

## MÓDULO 4: ESTRUCTURAS CONDICIONALES

**Descripción:** Aprenderás a tomar decisiones en tu código mediante if, else if, else, switch y el operador ternario. Este módulo también introduce el pattern matching de Java 17+, que permite evaluar patrones complejos en estructuras condicionales. Dominarás el flujo de control decisional, fundamental para cualquier programa.

1. Concepto de flujo de control en programación
2. La sentencia if básica
3. La sentencia if-else
4. La sentencia if-else if-else encadenada
5. Condiciones simples con operadores de igualdad y relacionales
6. Condiciones compuestas con && (AND lógico)
7. Condiciones compuestas con || (OR lógico)
8. Negación de condiciones con ! (NOT lógico)
9. Condiciones anidadas dentro de if
10. Bloques de código con {} y por qué siempre usarlos
11. Evaluación de short-circuit: cómo && y || detienen evaluación
12. Verificación de null antes de usar una variable
13. if (obj != null) pattern
14. El operador ternario como alternativa a if-else simple
15. Ternarios anidados (posible pero no recomendado)
16. La sentencia switch con enteros
17. Switch con bytes, shorts, chars
18. Switch con Strings (desde Java 7)
19. Switch con enums
20. La etiqueta default en switch
21. La palabra break en cada case
22. Fall-through: comportamiento cuando no hay break
23. Agrupación de múltiples case sin break
24. Cuándo el fall-through es intencional
25. Variables locales en un case y su scope (limitado)
26. Switch expressions (Java 14+)
27. Sintaxis de switch expression con ->
28. Switch expression con yield para bloques
29. Switch expression debe ser exhaustivo
30. Pattern matching for instanceof (Java 16+)
31. if (obj instanceof String s) { usar s }
32. Pattern matching con tipos de clase
33. Pattern matching con tipos de interfaz
34. Guarded patterns con && (Java 21)
35. Pattern matching en switch (Java 21)
36. Type pattern en switch: case String s ->
37. Null handling en pattern switch: case null ->
38. Guarded pattern en switch: case String s when s.length() > 5 ->
39. Pattern matching con sealed classes (Java 21)
40. Exhaustiveness checking con sealed types
41. Guard clauses: early return para simplificar lógica
42. Código defensivo y validación de parámetros
43. Cómo refactorizar if-else anidados
44. Replace nested conditionals with guard clauses
45. Cuándo usar switch vs if-else if
46. Cuándo usar switch expression vs switch statement
47. Polimorfismo como alternativa a switch con tipos
48. Map de acciones como alternativa a switch
49. Strategy pattern para reemplazar condicionales complejos
50. Comparar con null: == null vs Objects.isNull()
51. Comparar con null: != null vs Objects.nonNull()
52. Validación de cadenas: str == null || str.isEmpty()
53. Validación de cadenas con blank: str.isBlank() (Java 11+)
54. Condiciones con enumeraciones
55. Comparación case-insensitive en if con Strings
56. Condiciones con LocalDate: isBefore(), isAfter()
57. Condiciones con rangos de valores
58. Condiciones con colecciones: isEmpty(), contains()
59. Testing de condiciones: cómo probar todas las ramas
60. Cobertura de código y ramas condicionales
61. Complejidad ciclomática y condicionales
62. Principios para reducir la complejidad ciclomática
63. Code smell: demasiados if-else anidados
64. Code smell: switch con demasiados cases
65. Refactoring: Extract Method para simplificar condiciones
66. Refactoring: Replace Conditional with Polymorphism
67. Refactoring: Introduce Null Object
68. Refactoring: Replace Nested Conditional with Guard Clauses
69. Optional como alternativa a null checks
70. Optional.ifPresent() para ejecutar si no es null
71. Optional.orElse() para valor por defecto
72. Optional.map() para transformar condicionalmente
73. Optional.filter() para filtrar condicionalmente
74. Pattern matching con records (Java 21)
75. Record patterns: desestructurar records en patterns
76. Nested record patterns
77. Destructuring en switch con records
78. Boolean.getBoolean() para system properties
79. Comparación de enums con == (seguro y preferido)
80. Enum switch (exhaustivo por defecto)
81. Condiciones con expresiones regulares: matches()
82. Pattern.compile() para reutilizar patrones
83. Condiciones con colecciones: stream().anyMatch()
84. Condiciones con colecciones: stream().allMatch()
85. Condiciones con colecciones: stream().noneMatch()
86. Operaciones condicionales con Optional streams
87. Pattern matching con sealed interfaces (Java 21)
88. Switch expressions como expresiones (asignables)
89. Switch expressions con múltiples valores por case
90. Arrow form vs traditional form en switch
91. Ejemplo práctico: calculadora con switch expression
92. Ejemplo práptico: validación de formulario con guards
93. Ejemplo práctico: procesamiento de comandos con pattern matching
94. Ejemplo práctico: máquina de estados simple
95. Operaciones con booleanos: doble negación
96. Evitar != false, preferir simplemente la condición
97. Evitar == true, preferir simplemente la variable
98. Testing de null safety: assert null checks
99. NullAway y Checker Framework para null safety estático
100. Resumen y mejores prácticas para estructuras condicionales

---

## MÓDULO 5: BUCLES E ITERACIÓN

**Descripción:** Dominarás todas las estructuras de repetición de Java: for, while, do-while, for-each (enhanced for), y las nuevas funcionalidades de iteración. Aprenderás a controlar el flujo de los bucles con break y continue, a iterar sobre colecciones, a trabajar con bucles anidados y a optimizarlos.

1. Concepto de iteración y bucles en programación
2. La sentencia for: sintaxis y componentes
3. El inicializador del bucle for
4. La condición de continuación en for
5. El iterador (incremento/decremento) en for
6. Bucles for con incremento de más de uno
7. Bucles for con decremento (countdown)
8. Bucles for con paso negativo
9. Variables de control múltiples en for
10. for infinito: for(;;)
11. La sentencia while: sintaxis y uso
12. Diferencia entre for y while: cuándo usar cada uno
13. Bucles while que dependen de condiciones externas
14. La sentencia do-while
15. Diferencia entre while y do-while
16. Enhanced for loop (for-each): for (Tipo elem : coleccion)
17. for-each con arrays
18. for-each con List
19. for-each con Set
20. for-each con Map.entrySet()
21. for-each no permite modificar el índice
22. La palabra break: salir de un bucle
23. La palabra continue: saltar a la siguiente iteración
24. Diferencia entre break y continue
25. Bucles anidados
26. break y continue en bucles anidados (solo afectan al más interno)
27. Etiquetas (labels) con break y continue para bucles anidados
28. labeled break: OUTER: for (...) { break OUTER; }
29. Bucles infinitos y cómo evitarlos
30. Cómo depurar bucles con IntelliJ debugger
31. Puntos de interrupción (breakpoints) en bucles
32. Conditional breakpoints en IntelliJ
33. Evaluating expressions en el debugger
34. Iteración con índice usando for clásico
35. Iteración con índice usando for-each no es posible
36. Iterable<T> e Iterator<T>: qué hay detrás de for-each
37. Iterator: hasNext(), next(), remove()
38. Implementar Iterable<T> en una clase personalizada
39. Implementar Iterator<T> manualmente
40. Iterator y ConcurrentModificationException
41. No modificar colección durante iteración con for-each
42. Iterator.remove() como forma segura de eliminar
43. ListIterator para iteración bidireccional
44. Spliterator para iteración paralela (Java 8)
45. forEach() con Consumer (Java 8)
46. list.forEach(item -> System.out.println(item))
47. map.forEach((key, value) -> ...)
48. Iterable.forEach() como alternativa a for-each
49. Streams como alternativa a bucles (Java 8)
50. stream().forEach() vs for-each
51. Bucles con StringBuilder para construir strings grandes
52. Rendimiento: for vs for-each vs streams
53. for-each y la modificación de colecciones
54. for con List y acceso por índice
55. for con arreglos: array.length como condición
56. Bucles con expresiones regulares: Matcher.find()
57. Bucle infinito con while(true) y break
58. Patrón consumer-producer con while
59. Bucles y Thread.sleep() para temporización
60. Bucles con interruption (Thread.interrupted())
61. Parallel streams como alternativa a Parallel for
62. Bucles con recursividad como alternativa
63. Tail recursion y la falta de optimización en Java
64. StackOverflowError con recursión infinita
65. Bucle y Exception handling: try-catch dentro del bucle
66. Bucle y Exception handling: try-catch fuera del bucle
67. Patrón retry con bucle y contador
68. Bucles con IntStream.range() y IntStream.rangeClosed()
69. IntStream para iteración numérica funcional
70. LongStream y DoubleStream
71. Bucles y medición de tiempo: System.nanoTime()
72. Bucles y System.currentTimeMillis() (menos preciso)
73. Evitar trabajo innecesario dentro de bucles
74. Pre-computar el tamaño de una colección antes del bucle
75. Bucles para procesamiento de datos por lotes (batching)
76. Patrones de diseño que reemplazan bucles
77. Stream API para transformación de colecciones
78. map(), filter(), collect() como alternativa a bucles
79. Bucles con BufferedReader línea por línea
80. Bucles con Files.lines() (Java NIO)
81. Bucles con try-with-resources
82. Bucle y Progreso: imprimir avance porcentual
83. Bucle con barra de progreso en consola
84. Bucles y StringBuilder para construir CSV
85. for loop con múltiples condiciones
86. while con Scanner.hasNext() para leer input
87. Bucle para leer hasta centinela
88. Bucles y Optional: stream de optionals
89. Bucles y manejo de errores acumulados
90. Patrón de acumulación dentro de un bucle
91. Patrón de búsqueda dentro de un bucle
92. Patrón de filtrado dentro de un bucle
93. Patrón de transformación dentro de un bucle
94. Patrón de conteo dentro de un bucle
95. Enhanced for loop con tipos genéricos
96. Enhanced for loop con tipos primitivos en arrays
97. forEachRemaining() en Iterator
98. Enumeration (legacy) vs Iterator
99. for-each con colecciones concurrentes
100. Resumen y mejores prácticas para bucles

---

## MÓDULO 6: MÉTODOS Y FUNCIONES

**Descripción:** Los métodos son la unidad fundamental de organización del código en Java. Aprenderás a definir, llamar y sobrecargar métodos. Dominarás los parámetros, los valores de retorno, los métodos estáticos, y los aspectos avanzados como varargs, paso de parámetros, y métodos genéricos.

1. ¿Qué es un método y por qué usarlos?
2. Definir un método con tipo de retorno
3. Definir un método void (sin retorno)
4. Llamar a un método
5. Parámetros de entrada y su declaración
6. Paso por valor: Java siempre pasa por valor
7. Paso de primitivos: se copia el valor
8. Paso de objetos: se copia la referencia (no el objeto)
9. Parámetros con valores por defecto: Java NO tiene
10. Simular parámetros opcionales con sobrecarga
11. Varargs: parámetros variables con Tipo... args
12. Varargs debe ser el último parámetro
13. Varargs y el operador new en la llamada
14. Return statement: retorno explícito
15. Múltiples return statements en un método
16. Early return pattern (guard clauses)
17. Retorno de un solo valor (Java no tiene tuplas nativas)
18. Retorno con arrays o List para múltiples valores
19. Retorno con Records para múltiples valores (Java 16+)
20. Métodos estáticos (static)
21. Cuándo usar métodos estáticos vs de instancia
22. Clases de utilidad con solo métodos estáticos
23. Math como ejemplo de clase estática
24. Collections como ejemplo de clase estática
25. Methods con var (Java 10+, solo local)
26. Sobrecarga de métodos (overloading)
27. Sobrecarga con diferente número de parámetros
28. Sobrecarga con diferentes tipos de parámetros
29. Reglas de resolución de sobrecarga del compilador
30. Promoción de tipos en la resolución de sobrecarga
31. Ambigüedad en la sobrecarga de métodos
32. Sobrecarga de constructores
33. Constructor por defecto (sin parámetros)
34. Constructor parametrizado
35. Múltiples constructores (sobrecarga)
36. Constructor chaining con this()
37. this() debe ser la primera sentencia
38. Constructor de copia (no nativo, crear manualmente)
39. Inicializadores de instancia: { }
40. Inicializadores estáticos: static { }
41. Orden de inicialización: static init → instance init → constructor
42. Métodos como miembros de una clase
43. Acceso a campos de instancia desde métodos
44. La palabra clave this
45. this como referencia a la instancia actual
46. this para desambiguar campos de parámetros
47. this para llamar constructores: this(args)
48. this no se puede usar en métodos estáticos
49. Método main: punto de entrada de la aplicación
50. Argumentos de línea de comandos (String[] args)
51. Retorno de código de salida: System.exit(code)
52. Métodos de la clase Object: toString()
53. Métodos de la clase Object: equals(Object)
54. Métodos de la clase Object: hashCode()
55. Métodos de la clase Object: getClass()
56. Métodos de la clase Object: clone()
57. Métodos de la clase Object: finalize() (deprecated)
58. Métodos de la clase Object: wait(), notify(), notifyAll()
59. Recursividad: métodos que se llaman a sí mismos
60. StackOverflowError con recursión infinita
61. Caso base y caso recursivo
62. Ejemplo: factorial recursivo
63. Ejemplo: Fibonacci recursivo
64. Memoización manual para optimizar recursión
65. Métodos genéricos: <T> antes del tipo de retorno
66. Restricciones en métodos genéricos (bounds)
67. <T extends Comparable<T>>
68. Type inference en llamadas a métodos genéricos
69. Métodos con Optional<T> como retorno
70. Cuándo devolver null vs Optional
71. Métodos con tipos de retorno covariantes (no nativo en Java)
72. Método con atributo @Override
73. Método con atributo @Deprecated
74. Método con atributo @SuppressWarnings
75. Método con atributo @FunctionalInterface (en interfaces)
76. Métodos default en interfaces (Java 8)
77. Métodos estáticos en interfaces (Java 8)
78. Private methods en interfaces (Java 9)
79. Métodos abstractos (en clases abstractas)
80. Métodos con throws para declarar excepciones
81. Método con throws checked exception
82. Método con unchecked exception (no necesita throws)
83. Documentación Javadoc de métodos
84. @param, @return, @throws en Javadoc
85. Convenios de diseño de métodos: nombre verbo
86. Métodos que retornan this para fluent API
87. Builder pattern con métodos fluent
88. Métodos de fábrica estáticos: List.of(), Map.of()
89. Factory methods como alternativa a constructores
90. Companion methods (estáticos) en la misma clase
91. Utility methods en clases de utilidad
92. Singleton con constructor privado y método estático
93. Método estático con genéricos
94. Método de instancia con genéricos
95. Referencia a métodos: ClassName::methodName
96. Referencia a métodos de instancia: object::method
97. Referencia a constructores: ClassName::new
98. Method references como alternativa a lambdas
99. Method references con streams
100. Resumen: principios para diseñar buenos métodos

---

## MÓDULO 7: ARREGLOS (ARRAYS)

**Descripción:** Los arreglos son la estructura de datos más fundamental en Java. Aprenderás a crear, inicializar, recorrer y manipular arreglos unidimensionales y multidimensionales. Dominarás la clase Arrays del framework, los métodos de búsqueda, ordenación, copia, y las diferencias con las colecciones.

1. ¿Qué es un arreglo y por qué usarlo?
2. Declaración de arreglos: int[] nums o int nums[]
3. Creación con new: new int[5]
4. Inicialización inline: int[] nums = {1, 2, 3}
5. Inicialización con new: new int[]{1, 2, 3}
6. Acceso a elementos por índice [0]
7. Modificar elementos por índice
8. La propiedad length del arreglo (no es un método)
9. Índices fuera de rango: ArrayIndexOutOfBoundsException
10. Valores por defecto: 0, 0.0, false, null
11. Arreglos de tipos primitivos
12. Arreglos de Strings (tipos de referencia)
13. Arreglos de objetos
14. Arreglos de arreglos de objetos
15. Declaración con tipo explícito
16. var no funciona con inicialización de arreglos directamente
17. Recorrer con for clásico
18. Recorrer con for-each
19. Recorrer con for y length
20. Arreglos multidimensionales: int[][] matriz
21. Declaración de matrices 2D
22. Inicialización de matrices 2D: new int[filas][columnas]
23. Inicialización inline de matrices 2D
24. Acceso a elementos con [fila][columna]
25. Obtener dimensiones: matriz.length, matriz[0].length
26. Matrices irregulares (jagged arrays): filas de diferente tamaño
27. Recorrer matrices 2D con for anidados
28. Recorrer matrices 2D con for-each anidados
29. Arreglos tridimensionales: int[][][]
30. java.util.Arrays: la clase de utilidad
31. Arrays.sort() para ordenar
32. Arrays.sort() con Comparator personalizado
33. Arrays.binarySearch() en arreglos ordenados
34. Arrays.copyOf() para copiar
35. Arrays.copyOfRange() para copiar un rango
36. Arrays.fill() para llenar con un valor
37. Arrays.equals() para comparar arreglos
38. Arrays.deepEquals() para matrices
39. Arrays.toString() para representar como String
40. Arrays.deepToString() para matrices
41. Arrays.asList() para convertir a List
42. Arrays.stream() para convertir a Stream
43. Arrays.mismatch() para encontrar diferencia (Java 11)
44. Arrays.compare() para comparar (Java 9)
45. Arrays.setAll() para inicializar con función
46. Arrays.parallelSort() para ordenar en paralelo
47. System.arraycopy() para copia de bajo nivel
48. ArrayStoreException al guardar tipo incorrecto
49. Arreglos como parámetros de métodos
50. Arreglos como valor de retorno
51. Covarianza de arreglos en Java
52. El problema de la covarianza de arreglos
53. ArrayStoreException en covarianza
54. Arreglos y genéricos: no se puede crear new T[]
55. Arreglos y varargs: la relación
56. Arreglos de tipos genéricos: workarounds
57. Crear arreglos con streams: toArray()
58. IntStream.range() para generar secuencias
59. IntStream.rangeClosed() para generar secuencias inclusivas
60. Concatenar arreglos con streams
61. Distinct, filter con arreglos
62. List.of() como alternativa inmutable a arreglos
63. List.copyOf() para copia inmutable
64. Collections.unmodifiableList como alternativa
65. Arreglos readonly: no existe directamente en Java
66. Wrapping con Collections.unmodifiableList
67. Comparar arreglos: Arrays.equals() y Arrays.deepEquals()
68. Mezclar (shuffle) un arreglo con Collections.shuffle(List)
69. Encontrar mínimo y máximo manualmente
70. Arreglos de una sola dimensión vs matrices
71. Algoritmo de ordenación: Arrays.sort usa Dual-Pivot Quicksort
72. Implementar Comparable para ordenar objetos
73. Implementar Comparator para ordenar con lógica personalizada
74. Lambda con Comparator: Comparator.comparing()
75. Arreglos y serialización (Serializable)
76. Arreglos y JSON: Gson y Jackson
77. Rendimiento: acceso por índice vs for-each
78. Rendimiento: array vs ArrayList
79. Cuándo usar arreglos vs colecciones
80. Memory layout de arreglos en Java
81. Arreglos en el heap de la JVM
82. Arreglos de tipos primitivos: almacenamiento contiguo
83. Arreglos de objetos: almacenamiento de referencias
84. Arreglos grandes y OutOfMemoryError
85. -Xmx y tamaño máximo de arreglos
86. Integer.MAX_VALUE como límite de tamaño
87. Arreglos y la clase ArrayList como wrapper
88. Convertir de List a array: list.toArray(new T[0])
89. Convertir de array a List: Arrays.asList()
90. Arrays.asList() devuelve una lista fija (no resizable)
91. new ArrayList<>(Arrays.asList()) para lista resizable
92. List.of() para lista inmutable
93. Arreglos de enums
94. Arreglos y genéricos con wildcards
95. Arreglos y casting de tipos
96. Arreglos y Thread safety
97. Arreglos compartidos entre threads
98. AtomicIntegerArray para arreglos thread-safe
99. CopyOnWriteArrayList como alternativa thread-safe
100. Resumen y mejores prácticas con arreglos

---

## MÓDULO 8: STRINGS Y MANIPULACIÓN DE TEXTO

**Descripción:** Los Strings son omnipresentes en Java. Dominarás la clase String, sus métodos fundamentales, los diferentes tipos de literales de cadena, la comparación eficiente, la manipulación de texto, StringBuilder/StringBuffer para rendimiento, y los aspectos de internacionalización.

1. La clase String y java.lang.String
2. Strings como objetos (tipos de referencia)
3. Inmutabilidad de los Strings en Java
4. Declaración e inicialización de Strings
5. Literales de cadena: "texto"
6. El String Pool: reutilización de literales
7. new String("texto") vs "texto": la diferencia
8. == compara referencias, .equals() compara contenido
9. .equals() para comparación de contenido
10. .equalsIgnoreCase() para comparación sin case
11. .compareTo() para comparación lexicográfica
12. Text blocks (Java 15): """..."""
13. Text blocks con formato y alineación
14. Secuencias de escape: \n, \t, \\, \"
15. Secuencias de escape en text blocks: \n es opcional
16. Concatenación con el operador +
17. Concatenación con .concat()
18. StringBuilder para concatenación eficiente
19. StringBuilder: append(), insert(), delete(), replace()
20. StringBuilder: reverse(), toString()
21. StringBuilder: capacity() y length()
22. StringBuilder vs StringBuffer (thread-safe)
23. StringBuffer: sincronizado pero más lento
24. Cuándo usar StringBuilder vs StringBuffer
25. String.valueOf() para convertir a String
26. Integer.toString(), Double.toString()
27. String.format() para formateo estilo printf
28. Especificadores: %d, %f, %s, %b, %n
29. System.out.printf() para imprimir formateado
30. MessageFormat para formato con argumentos
31. Propiedad length(): .length() (es un método)
32. Acceso a caracteres por índice: .charAt(0)
33. Strings NO soportan operador [] (no es array)
34. String vacío: ""
35. String.isBlank() (Java 11): vacío o solo espacios
36. String.isEmpty(): solo si length == 0
37. null vs "" vs " " : las tres son diferentes
38. Métodos de búsqueda: .contains()
39. Métodos de búsqueda: .startsWith()
40. Métodos de búsqueda: .endsWith()
41. Métodos de búsqueda: .indexOf()
42. Métodos de búsqueda: .lastIndexOf()
43. Métodos de búsqueda con posición: .indexOf("x", fromIndex)
44. Métodos de transformación: .toLowerCase()
45. Métodos de transformación: .toUpperCase()
46. Métodos de transformación: .trim() (elimina espacios extremos)
47. Métodos de transformación: .strip() (Java 11, Unicode-aware)
48. .stripLeading() y .stripTrailing() (Java 11)
49. Métodos de transformación: .replace()
50. Métodos de transformación: .replaceAll() con regex
51. Métodos de transformación: .replaceFirst() con regex
52. Métodos de transformación: .substring(startIndex)
53. Métodos de transformación: .substring(start, end)
54. .toCharArray() para convertir a char[]
55. Dividir strings con .split(regex)
56. .split() con límite de partes
57. Unir strings con String.join()
58. String.join() con delimitador
59. String.join() con colección
60. .chars() para obtener IntStream de caracteres
61. .codePoints() para obtener IntStream de code points
62. chars() y codePoints() con streams para procesamiento
63. .repeat(n) para repetir (Java 11)
64. .indent(n) para agregar indentación (Java 12)
65. .transform() para aplicar función (Java 12)
66. .describeConstable() y .resolveConstantDesc() (Java 12)
67. char.IsLetter(), Character.isDigit()
68. Character.isWhitespace(), Character.isUpperCase()
69. Character.toUpperCase(), Character.toLowerCase()
70. Character.isLetterOrDigit()
71. Encoding: UTF-8, UTF-16, ISO-8859-1
72. String.getBytes() con charset
73. new String(bytes, charset)
74. StandardCharsets.UTF_8 como constante
75. Unicode y los diferentes code points
76. Supplementary characters y surrogate pairs
77. String interning: String.intern()
78. String pool y literales
79. String concatenation en bucles: StringBuilder
80. El compilador optimiza concatenación simple con +
81. El compilador NO optimiza concatenación en bucles
82. Constantes de String y el compilador
83. String normalization: Normalizer.normalize()
84. Unicode NFC y NFD
85. Cultura y comparación de Strings
86. Collator para comparación localizada
87. DecimalFormat para formato numérico
88. DateFormat para formato de fechas
89. Truncar strings de forma segura
90. Reverse de un String (con StringBuilder)
91. Contar ocurrencias de un carácter
92. Contar ocurrencias de un substring
93. Validar si un String es numérico
94. isNumeric con Character.isDigit()
95. String hashing: .hashCode()
96. Strings en colecciones y hash code
97. HashSet<String> y HashMap<String, V>
98. String como key en HashMap
99. Comparar por cultura con Collator
100. Resumen y mejores prácticas con Strings

---

## MÓDULO 9: FECHA, HORA Y TIPOS NUMÉRICOS

**Descripción:** Trabajar con fechas, horas y números requiere precisión. Este módulo cubre la API java.time (LocalDate, LocalDateTime, ZonedDateTime, Duration, Period), los tipos numéricos en profundidad, BigDecimal/BigInteger, y los formatos de presentación. Aprenderás a manejar zonas horarias y los problemas comunes con datos temporales.

1. java.time: la API moderna de fecha y hora (Java 8)
2. LocalDate: solo fecha, sin hora
3. LocalDate.now() y LocalDate.of(año, mes, día)
4. LocalDate.parse("2024-01-15")
5. Propiedades: getYear(), getMonthValue(), getDayOfMonth()
6. getDayOfWeek(), getDayOfYear()
7. LocalDate.isLeapYear()
8. LocalDate.lengthOfMonth()
9. Operaciones con LocalDate: plusDays(), minusDays()
10. plusMonths(), minusMonths(), plusYears(), minusYears()
11. LocalDate.withYear(), withMonth(), withDayOfMonth()
12. LocalDate.with(TemporalAdjusters)
13. TemporalAdjusters: firstDayOfMonth(), lastDayOfMonth()
14. TemporalAdjusters: next(DayOfWeek.MONDAY)
15. Comparar fechas: isBefore(), isAfter(), isEqual()
16. LocalDate.until() para obtener Period
17. LocalTime: solo hora, sin fecha
18. LocalTime.now() y LocalTime.of(hora, minuto)
19. LocalTime.of(hora, minuto, segundo, nano)
20. Operaciones con LocalTime: plusHours(), minusMinutes()
21. LocalTime.MIDNIGHT, NOON
22. LocalDateTime: fecha y hora sin zona
23. LocalDateTime.now()
24. LocalDateTime.of(LocalDate, LocalTime)
25. LocalDateTime.parse("2024-01-15T10:30:00")
26. Operaciones con LocalDateTime
27. ZonedDateTime: fecha, hora y zona
28. ZonedDateTime.now()
29. ZonedDateTime.now(ZoneId.of("America/New_York"))
30. ZoneId.getAvailableZoneIds()
31. ZoneId.systemDefault()
32. Convertir entre zonas: withZoneSameInstant()
33. OffsetDateTime y OffsetTime
34. Diferencia entre ZonedDateTime y OffsetDateTime
35. Instant: un punto en el tiempo (timestamp)
36. Instant.now() y Instant.ofEpochSecond()
37. Instant.toEpochMilli()
38. Instant para almacenar timestamps
39. Duration: cantidad de tiempo (horas, minutos, segundos)
40. Duration.between(temporal1, temporal2)
41. Duration.ofHours(), ofMinutes(), ofSeconds()
42. Duration: toHours(), toMinutes(), toSeconds()
43. Period: cantidad de tiempo (años, meses, días)
44. Period.between(localDate1, localDate2)
45. Period.ofYears(), ofMonths(), ofDays()
46. Duration vs Period: cuándo usar cada uno
47. DateTimeFormatter para formateo
48. DateTimeFormatter.ofPattern("yyyy-MM-dd")
49. Especificadores: y, M, d, H, h, m, s, S
50. DateTimeFormatter.ISO_LOCAL_DATE
51. DateTimeFormatter.ISO_LOCAL_DATE_TIME
52. Formateo: localDate.format(formatter)
53. Parsing: LocalDate.parse(str, formatter)
54. DateTimeFormatter con Locale
55. DateTimeFormatterBuilder para formatos complejos
56. java.util.Date (legacy): evitar
57. java.util.Calendar (legacy): evitar
58. java.text.SimpleDateFormat (legacy): evitar
59. Conversión de legacy a java.time
60. Date.from(Instant) y Date.toInstant()
61. Timestamp y java.time
62. NodaTime como alternativa a java.time
63. ISO 8601 como formato estándar
64. Almacenar fechas en UTC
65. Presentar fechas en zona local
66. El problema de las zonas horarias y DST
67. Daylight Saving Time y java.time
68. Tipos numéricos enteros: byte, short, int, long
69. byte (-128 a 127)
70. short (-32768 a 32767)
71. int y long: los más usados
72. BigInteger para números arbitrariamente grandes
73. Tipos de punto flotante: float y double
74. Precisión de float: ~6-9 dígitos
75. Precisión de double: ~15-17 dígitos
76. Cuándo usar float vs double
77. Problemas de precisión con float y double
78. BigDecimal para precisión exacta
79. BigDecimal para cálculos financieros
80. BigDecimal: add, subtract, multiply, divide
81. BigDecimal.setScale() y RoundingMode
82. BigDecimal.valueOf() vs new BigDecimal()
83. Math.abs(), Math.min(), Math.max()
84. Math.floor(), Math.ceil(), Math.round()
85. Math.pow(), Math.sqrt(), Math.log()
86. Math.PI y Math.E
87. Math.toIntExact() para casting seguro de long a int
88. Math.addExact(), Math.multiplyExact() con overflow check
89. Integer.MAX_VALUE y Integer.MIN_VALUE
90. Long.MAX_VALUE y Long.MIN_VALUE
91. Double.MAX_VALUE, Double.MIN_VALUE
92. Double.POSITIVE_INFINITY, Double.NEGATIVE_INFINITY
93. Double.NaN y Double.isNaN()
94. Comparación de doubles con epsilon
95. Formateo numérico: DecimalFormat
96. NumberFormat.getCurrencyInstance()
97. NumberFormat.getPercentInstance()
98. Locale y formato numérico
99. Random: generación de números aleatorios
100. Resumen: cuándo usar cada tipo numérico y temporal

---

## MÓDULO 10: POO - CLASES Y OBJETOS

**Descripción:** Este módulo introduce el paradigma de Programación Orientada a Objetos desde Java. Aprenderás a definir clases, crear objetos, entender la diferencia entre tipos de referencia y valor, trabajar con campos, métodos, constructores, y la palabra clave this. Java es un lenguaje puramente orientado a objetos (excepto primitivos).

1. ¿Qué es la Programación Orientada a Objetos (POO)?
2. Los cuatro pilares de POO: encapsulamiento, herencia, polimorfismo, abstracción
3. Clases como plantillas para objetos
4. Objetos como instancias de clases
5. Declarar una clase con la palabra class
6. Miembros de una clase: campos, métodos, constructores
7. Campos (fields/instance variables) y su declaración
8. Convención: camelCase para campos
9. Campos estáticos (static variables)
10. Campos finales (final) y constantes
11. Campos con valores por defecto: 0, 0.0, false, null
12. Métodos: la interfaz de la clase
13. Métodos de instancia vs métodos estáticos
14. Constructores: el método especial de inicialización
15. Constructor por defecto (sin parámetros)
16. Constructor parametrizado
17. Múltiples constructores (sobrecarga)
18. Constructor chaining con this()
19. Constructores y el orden de inicialización
20. Inicializadores de instancia: { }
21. Inicializadores estáticos: static { }
22. Orden: static init → instance init → constructor
23. Bloques de inicialización y constructores juntos
24. Crear objetos con new
25. new Persona("Ana", 30)
26. Asignación de objetos: se asigna la referencia
27. null para referencias sin objeto
28. NullPointerException y cómo prevenirlo
29. Comparación de objetos: == vs .equals()
30. == compara referencias
31. .equals() compara contenido
32. Override de .equals() y .hashCode()
33. El contrato entre equals() y hashCode()
34. Override de .toString()
35. Object como la raíz de todas las clases
36. Herencia implícita de Object
37. getClass() para obtener el tipo en runtime
38. Modificadores de acceso: public, private, protected
39. Default (package-private): sin modificador
40. Tabla de niveles de acceso en Java
41. Principio de menor visibilidad
42. Java NO tiene modificador "internal" como C#
43. Java NO tiene modificador "file" como C# 11
44. Clases anidadas estáticas (static nested classes)
45. Clases internas (inner classes / non-static nested)
46. Clases locales (dentro de métodos)
47. Clases anónimas: new Interface() { ... }
48. Cuándo usar cada tipo de clase anidada
49. El acceso a miembros de la clase exterior desde inner class
50. Outer.this para referenciar la clase exterior
51. Enum como tipo especial de clase
52. Declarar un enum: enum Color { RED, GREEN, BLUE }
53. Enums con campos, constructores y métodos
54. Enums con métodos abstractos
55. Enum.values(), valueOf(), ordinal()
56. Enum en switch statements
57. Enums implementan interfaces
58. Enums como singletons
59. Records (Java 16+): clases inmutables para datos
60. record Persona(String nombre, int edad)
61. Records: equals(), hashCode(), toString() automáticos
62. Records con custom constructors
63. Records con métodos personalizados
64. Records: compact canonical constructor
65. Records implementan interfaces
66. Records y pattern matching
67. Sealed classes (Java 17+): controlar herencia
68. sealed class Shape permits Circle, Rectangle
69. sealed interface permits ...
70. non-sealed y final en la jerarquía
71. Sealed classes y pattern matching exhaustivo
72. Sealed classes y records juntos
73. Clases abstractas (introducción, M15 profundiza)
74. Interfaces (introducción, M14 profundiza)
75. El ciclo de vida de un objeto
76. Garbage Collector: introducción
77. El GC libera objetos sin referencias
78. finalize() está deprecated: no usarlo
79. Cleaners como alternativa (Java 9+)
80. Try-with-resources y AutoCloseable
81. Implementar AutoCloseable
82. Closable vs AutoCloseable
83. Tipos por valor: primitivos (siempre en stack)
84. Tipos por referencia: objetos (siempre en heap)
85. Java no tiene structs como C#
86. Value types: Proyecto Valhalla (futuro de Java)
87. Domain modeling con clases
88. Value Objects: objetos inmutables por valor
89. Entities: objetos con identidad
90. Ejemplo: clase Persona con propiedades y métodos
91. Ejemplo: clase Producto con validación
92. Ejemplo: clase CuentaBancaria con encapsulamiento
93. Ejemplo: clase Calculadora con métodos estáticos
94. Ejemplo: clase Carro con composición
95. Override de toString() para debugging
96. Override de equals() y hashCode()
97. Implementar Comparable<T>
98. Implementar Comparator<T>
99. UML básico: diagrama de clases
100. Resumen: principios para diseñar buenas clases

---

## MÓDULO 11: ENCAPSULAMIENTO Y MODIFICADORES DE ACCESO

**Descripción:** El encapsulamiento es el pilar que protege el estado interno de un objeto. Aprenderás en profundidad todos los niveles de visibilidad de Java, cómo ocultar la implementación interna, exponer solo lo necesario a través de getters/setters y métodos públicos, y las mejores prácticas de diseño.

1. ¿Qué es el encapsulamiento y por qué es fundamental?
2. Ocultar la implementación: información que debe ser privada
3. Interfaz pública vs implementación privada
4. Modificador public: acceso desde cualquier lugar
5. Modificador private: acceso solo dentro de la clase
6. Modificador protected: acceso en la clase, subclases y mismo package
7. Default (package-private): acceso solo dentro del package
8. Tabla resumen de niveles de acceso
9. Diferencia entre protected de Java y protected de C#
10. Java no tiene internal, private protected como C#
11. Cuándo usar cada modificador de acceso
12. Principio de mínimo privilegio
13. Campos privados como backing fields
14. Getters y setters: métodos de acceso
15. Getter con convención getNombre()
16. Setter con convención setNombre(valor)
17. Getters para boolean: isActivo()
18. Propiedades de solo lectura: solo getter, sin setter
19. Propiedades de solo escritura: solo setter (raro)
20. Java no tiene propiedades como C#: simular con métodos
21. JavaBeans specification: get/set pattern
22. Bean properties y frameworks que las usan
23. Lombok: @Getter, @Setter para generar getters/setters
24. Lombok: @Data para generar todo
25. Lombok: @Value para clases inmutables
26. @AllArgsConstructor y @NoArgsConstructor de Lombok
27. @Builder de Lombok para patrón builder
28. Constructores públicos vs factory methods
29. Constructores privados y factory methods
30. Singleton con constructor privado
31. Readonly fields con final
32. final fields: asignables en declaración o constructor
33. final y la inmutabilidad
34. final en métodos: impedir override
35. final en clases: impedir herencia
36. final parameters: no reasignar parámetros
37. Inmutabilidad: diseño de clases inmutables
38. Class inmutables con final class, final fields, sin setters
39. Records como clases inmutables (Java 16+)
40. Builder pattern para construir objetos inmutables
41. Data Transfer Objects (DTOs) inmutables
42. Collection properties: exponer como List (no ArrayList)
43. No exponer arrays directamente
44. No exponer colecciones mutables directamente
45. Collections.unmodifiableList() para listas de solo lectura
46. List.of() para listas inmutables
47. Map.of() para mapas inmutables
48. Set.of() para sets inmutables
49. Defensive copy al devolver colecciones mutables
50. Defensive copy al recibir colecciones mutables
51. Encapsular lógica de negocio en métodos
52. Evitar anemic domain model
53. State pattern para encapsular estados
54. Validación en el constructor
55. Validación en setters
56. Objects.requireNonNull() para validación de null
57. Factory methods para controlar creación
58. Constructor privado y static factory
59. Properties que dependen de otras
60. Lazy initialization con Supplier
61. Encapsular cambio de estado: métodos con nombre descriptivo
62. Command pattern para encapsular acciones
63. Value Objects como objetos inmutables
64. Strong typing: evitar "stringly typed" code
65. Wrapper types para tipos primitivos
66. Type-safe identifiers
67. Generics como forma de encapsular tipos
68. Interfaces como contrato de encapsulamiento
69. @VisibleForTesting de Guava (convención)
70. Encapsulamiento en registros (Records)
71. Records: todos los campos son private final
72. Records con custom getters (method name = field name)
73. Encapsulamiento y JavaBeans
74. Encapsulamiento y Spring (dependency injection)
75. @Autowired en campos (field injection - no recomendado)
76. Constructor injection (recomendado)
77. Setter injection como alternativa
78. Encapsulamiento y JPA/Hibernate
79. Entity con campos privados y getters/setters
80. Backing fields en JPA
81. Encapsulamiento en APIs REST: no exponer entidades directamente
82. DTOs vs Entidades: cuándo usar cada uno
83. ViewModels como encapsulamiento de presentación
84. ModelMapper o MapStruct para mapeo entre capas
85. Encapsulamiento y change tracking
86. INotifyPropertyChanged (no existe en Java desktop, pero sí en Android)
87. Encapsulamiento en clases de utilidad
88. Constructor privado en clases de utilidad
89. Encapsulamiento y thread safety
90. volatile keyword y campos
91. synchronized para métodos thread-safe
92. AtomicReference para campos thread-safe
93. Encapsulamiento en serialización
94. @JsonProperty y @JsonIgnore (Jackson)
95. @Expose de Gson
96. Jakarta Validation para validación
97. @NotNull, @Size, @Min, @Max
98. Encapsulamiento y SRP (Single Responsibility)
99. Tell, Don't Ask principle
100. Resumen: reglas de encapsulamiento para diseño limpio

---

## MÓDULO 12: HERENCIA Y COMPOSICIÓN

**Descripción:** La herencia permite crear jerarquías de clases que comparten comportamiento. Aprenderás a usar la herencia en Java, la keyword super, constructores en jerarquías, casting entre tipos, y fundamentalmente cuándo preferir la composición sobre la herencia.

1. ¿Qué es la herencia y para qué sirve?
2. Clase base (padre/superclase) y clase derivada (hija/subclase)
3. Sintaxis de herencia con extends
4. Herencia simple en Java (no multiple inheritance de clases)
5. La clase Object como raíz de todas las clases
6. Miembros heredados: campos, métodos
7. Miembros no heredados: constructores y private members
8. Modificadores de acceso en herencia: public, protected, private
9. private members: no accesibles desde la subclase
10. protected members: accesibles desde la subclase y mismo package
11. La palabra clave super para acceder a la superclase
12. Llamar al constructor padre con super()
13. super() debe ser la primera sentencia del constructor
14. Constructores parametrizados y la cadena de llamadas
15. Constructor por defecto implícito y la jerarquía
16. Si la superclase no tiene constructor por defecto, la subclase debe llamar super(args)
17. Métodos heredados y su sobrescritura (override)
18. La anotación @Override
19. Reglas para override: mismo nombre, parámetros y tipo de retorno
20. Reglas de acceso: no se puede reducir la visibilidad
21. Reglas de excepciones en override
22. Covariant return types en override
23. La palabra final para impedir override
24. La palabra final para impedir herencia de la clase
25. La palabra final en métodos individuales
26. Casting de subclase a superclase (upcasting, implícito)
27. Casting de superclase a subclase (downcasting, explícito)
28. ClassCastException y cómo evitarlo
29. El operador instanceof para verificar tipo
30. Pattern matching for instanceof (Java 16+)
31. getClass() para obtener el tipo real en runtime
32. Jerarquías profundas: pros y contras
33. Composición sobre herencia: principio fundamental
34. ¿Qué es la composición?
35. Has-A vs Is-A: cuándo usar cada relación
36. Delegación: pasar trabajo a un objeto interno
37. Wrapping: decorar un objeto con funcionalidad extra
38. Decorator pattern usando composición
39. Strategy pattern usando composición
40. Favor composition over inheritance (GoF)
41. Herencia de implementación vs herencia de tipo
42. Interfaces como herencia de tipo sin implementación
43. Herencia con clases abstractas (introducción)
44. Herencia con interfaces múltiples
45. Cuándo la herencia es la elección correcta
46. Frameworks que requieren herencia
47. Template Method pattern con herencia
48. Abstract base classes como plantillas
49. Herencia y serialización
50. Herencia y JSON (Jackson, Gson)
51. @JsonTypeInfo y @JsonSubTypes (Jackson)
52. Herencia y JPA/Hibernate
53. @Inheritance: SINGLE_TABLE, JOINED, TABLE_PER_CLASS
54. @DiscriminatorColumn y @DiscriminatorValue
55. Herencia y Java Collections Framework
56. AbstractList, AbstractMap como ejemplos
57. Herencia en el framework: Exception hierarchy
58. Herencia en el framework: InputStream/OutputStream
59. Herencia en el framework: Reader/Writer
60. Herencia y testing: testear jerarquías
61. Evitar la herencia excesiva: shallow hierarchies
62. Liskov Substitution Principle (LSP)
63. Violaciones comunes de LSP
64. Precondiciones y postcondiciones en herencia
65. Herencia de interfaces (interface extends interface)
66. Multiple interface inheritance
67. Default methods y el diamond problem
68. Herencia con records (records son final por defecto)
69. Sealed classes para controlar herencia
70. sealed, permits, non-sealed, final
71. Herencia y generics: <T extends BaseClass>
72. Bounded type parameters
73. Wildcards: <? extends BaseClass>
74. <? super BaseClass>
75. PECS: Producer Extends, Consumer Super
76. Upcasting y downcasting en colecciones genéricas
77. Generics y erasure: implicaciones en herencia
78. Reflection y herencia: getSuperclass()
79. Reflection: getDeclaredMethods() vs getMethods()
80. Herencia y Attributes: meta-annotations
81. @Inherited annotation
82. Herencia y el patrón Template Method
83. Herencia y el patrón Factory Method
84. Herencia y el patrón Observer
85. Acoplamiento y cohesión en herencia vs composición
86. Dependency inversion: depender de abstracciones
87. Refactoring: Replace Inheritance with Delegation
88. Refactoring: Extract Superclass
89. Refactoring: Pull Up Method / Push Down Method
90. Composition root con DI containers
91. Spring y composición con @Component
92. Spring y herencia con extends
93. Herencia y testing con mocks
94. Mockito y clases concretas (limitaciones)
95. Preferir interfaces para mockability
96. Herencia y Java Streams
97. Herencia y Optional
98. Herencia y Exceptions (custom exceptions)
99. Design guidelines: shallow hierarchies, interfaces first
100. Resumen: reglas para decidir herencia vs composición

---

## MÓDULO 13: POLIMORFISMO

**Descripción:** El polimorfismo permite que objetos de diferentes tipos se traten de manera uniforme. Aprenderás polimorfismo de herencia (dynamic dispatch), polimorfismo de sobrecarga (overloading), polimorfismo paramétrico (generics), y polimorfismo de interfaz.

1. ¿Qué es el polimorfismo y por qué es esencial?
2. Los tipos de polimorfismo en Java
3. Polimorfismo de herencia (runtime polymorphism)
4. Polimorfismo de sobrecarga (compile-time polymorphism)
5. Polimorfismo paramétrico (generics)
6. Polimorfismo de interfaz
7. Override de métodos y dynamic dispatch
8. Dynamic dispatch: cómo la JVM elige el método correcto
9. Static dispatch: cómo el compilador elige el método
10. Calling a overridden method on a superclass reference
11. Upcasting: asignar un subtipo a una variable supertipo
12. Downcasting con cast explícito
13. Downcasting seguro con instanceof
14. Pattern matching instanceof como alternativa a casting
15. Liskov Substitution Principle (LSP)
16. LSP: un subtipo debe poder sustituir a su supertipo
17. Violaciones de LSP y cómo detectarlas
18. final methods: impedir override
19. final classes: impedir herencia
20. Sobrecarga de métodos (overloading)
21. Resolución de sobrecarga por el compilador
22. Sobrecarga con diferente número de parámetros
23. Sobrecarga con diferentes tipos de parámetros
24. Ambigüedad en la sobrecarga
25. Método más específico: reglas de resolución
26. Polimorfismo paramétrico con generics
27. Generic methods con tipo en tiempo de compilación
28. Generic classes con tipo parametrizado
29. Bounded type parameters para limitar polimorfismo
30. Wildcards: <?>, <? extends T>, <? super T>
31. PECS: Producer Extends, Consumer Super
32. Polimorfismo con interfaces
33. Implementación de interfaz en múltiples clases
34. Llamar a través de referencia de interfaz
35. Implementación de múltiples interfaces
36. Interfaces como contrato polimórfico
37. Polimorfismo con clases abstractas
38. Abstract methods que fuerzan implementación
39. Abstract classes vs interfaces: cuándo usar cada una
40. Template Method pattern: polimorfismo con plantilla
41. Strategy pattern: polimorfismo con estrategias
42. Factory pattern: crear objetos polimórficos
43. Polymorphic collections: List<Animal> con perros y gatos
44. Polimorfismo y el operador instanceof
45. Polimorfismo y el operador getClass()
46. Polimorfismo con sealed classes y permits
47. Polimorfismo con records
48. Polimorfismo y el patrón State
49. Polimorfismo y el patrón Command
50. Polimorfismo y el patrón Chain of Responsibility
51. Polimorfismo en el framework: InputStream, OutputStream
52. Polimorfismo en el framework: List, Set, Map
53. Polimorfismo en el framework: javax.servlet
54. Polimorfismo en Spring: @Component, @Service
55. Polimorfismo en Spring: inyección por tipo
56. Polimorfismo en JPA: entity inheritance
57. Polimorfismo en APIs REST
58. Discriminated unions con sealed classes
59. Double dispatch problem en Java
60. Visitor pattern para double dispatch
61. Performance: virtual dispatch vs direct call
62. JIT devirtualization
63. final methods y classes para devirtualization
64. Inlining y métodos virtuales
65. Polimorfismo y testing: mock objects
66. Polimorfismo y DI: resolver tipos en runtime
67. Polimorfismo y Open/Closed Principle
68. Open/Closed con herencia
69. Open/Closed con composición e interfaces
70. Polimorfismo vs pattern matching: cuándo usar cada uno
71. Switch con instanceof patterns (Java 21)
72. Polimorfismo con lambdas y functional interfaces
73. Function<T, R> como polimorfismo funcional
74. Predicate<T> como polimorfismo funcional
75. Consumer<T> y Supplier<T>
76. Polimorfismo con streams
77. Polimorfismo con Optional
78. Polimorfismo en serialización (Jackson, Gson)
79. Polimorfismo en testing con mocks
80. Refactoring: Replace Conditional with Polymorphism
81. Refactoring: Extract Interface
82. Code smell: type checking con múltiples instanceof
83. Anti-pattern: God class
84. Polimorfismo y SRP
85. Polimorfismo y DIP
86. Polimorfismo y ISP
87. Polimorfismo en Java Collections Framework
88. Polimorfismo en Java Streams
89. Polimorfismo en Java I/O
90. Polimorfismo en event handling
91. Polimorfismo en listeners
92. Polimorfismo en callbacks
93. Polimorfismo con anonymous classes
94. Polimorfismo con lambdas
95. Polimorfismo con method references
96. Polimorfismo y generics: bounded wildcards
97. Polimorfismo y generics: type erasure
98. Polimorfismo en Jakarta EE / Spring
99. Polimorfismo en microservices
100. Resumen: principios para diseño polimórfico limpio

---

## MÓDULO 14: INTERFACES

**Descripción:** Las interfaces definen contratos que las clases deben cumplir. Aprenderás a diseñar, implementar y usar interfaces en Java, desde la sintaxis básica hasta las default methods de Java 8, static methods en interfaces, private methods en interfaces, y patrones de diseño basados en interfaces.

1. ¿Qué es una interfaz y por qué es fundamental?
2. Definir una interfaz: sintaxis con interface
3. Convención de nombres: I al inicio o nombre descriptivo
4. Métodos abstractos en interfaces (implícitamente public abstract)
5. Constantes en interfaces (implícitamente public static final)
6. Implementar una interfaz con implements
7. Implementar múltiples interfaces
8. Una clase puede implementar muchas interfaces
9. Una interfaz puede extender otra interfaz
10. Una interfaz puede extender múltiples interfaces
11. Interfaces como tipo de referencia
12. Asignar una clase a una variable de tipo interfaz
13. Interfaces en parámetros de métodos
14. Interfaces como tipo de retorno
15. Interfaces en colecciones: List<Animal>
16. Interfaces y polimorfismo
17. Interfaces y Dependency Injection
18. Interfaces como abstracciones
19. Interfaz vs clase abstracta: diferencias
20. Cuándo usar interfaz vs clase abstracta
21. Default methods (Java 8): interface con implementación
22. Sintaxis: default ReturnType methodName() { }
23. Override de default methods en clases
24. El problema del diamante con default methods
25. Resolver el diamante: override obligatorio
26. Static methods en interfaces (Java 8)
27. Private methods en interfaces (Java 9)
28. Private static methods en interfaces (Java 9)
29. Private methods para compartir lógica entre default methods
30. Interfaces genéricas: Comparable<T>, Iterable<T>
31. Interfaces genéricas con bounded type parameters
32. Implementar interfaces genéricas con tipos concretos
33. Wildcards con interfaces genéricas
34. Interfaces comunes del framework: Comparable<T>
35. Comparator<T>
36. Iterable<T> e Iterator<T>
37. Collection<E>, List<E>, Set<E>, Map<K,V>
38. Serializable y Cloneable (marker interfaces)
39. AutoCloseable y Closeable
40. Runnable y Callable<V>
41. Function<T, R>, Predicate<T>, Consumer<T>, Supplier<T>
42. ActionListener (Swing/legacy)
43. Function interfaces (@FunctionalInterface)
44. @FunctionalInterface annotation
45. Functional interfaces y lambdas
46. Samos (Single Abstract Method) interfaces
47. Interfaces marker: Serializable (sin métodos)
48. Marker interfaces vs annotations
49. Interface segregation principle (ISP)
50. Diseñar interfaces pequeñas y específicas
51. Code smell: interfaz gorda (fat interface)
52. Refactoring: Split Interface
53. Refactoring: Extract Interface
54. Dependency Inversion Principle (DIP)
55. Depender de abstracciones, no de concreciones
56. Interfaces en la capa de aplicación
57. Interfaces en la capa de dominio
58. Repository pattern con interfaces
59. Service interfaces para DI
60. Mock de interfaces para testing
61. Mockito: when(mock.method()).thenReturn(value)
62. Interfaces y Fluent APIs
63. Fluent interface pattern
64. Builder pattern con interfaces
65. Chain of responsibility con interfaces
66. Strategy pattern con interfaces
67. Adapter pattern con interfaces
68. Decorator pattern con interfaces
69. Composite pattern con interfaces
70. Observer pattern con interfaces
71. Command pattern con interfaces
72. Factory pattern con interfaces
73. Interfaces para testing: abstraer I/O
74. Interfaces para abstraer base de datos
75. Interface de dominio vs interfaz de infraestructura
76. Pattern matching con interfaces (Java 21)
77. instanceof InterfaceName
78. Casting a interfaz
79. Interfaces y extension methods (no existen en Java)
80. Interfaces y static factory methods
81. Sealed interfaces (Java 17)
82. sealed interface Shape permits Circle, Rectangle
83. Interfaces con default methods y versioning
84. Evolución de interfaces sin romper compatibilidad
85. Interfaces en API design
86. SPI (Service Provider Interface) pattern
87. ServiceLoader con interfaces
88. Plug-in architecture con interfaces
89. Interfaces y reflection
90. getInterfaces() para obtener interfaces implementadas
91. isAssignableFrom() para verificar implementación
92. Interfaces y serialización
93. Interfaces y JSON (Jackson, Gson)
94. Interfaces y Spring: @Component implements Service
95. Interfaces y JPA: no se persisten
96. Interfaces y generics avanzado
97. Recursive type bounds con interfaces
98. Interface con métodos default que llaman abstract methods
99. Anti-pattern: Service Locator
100. Resumen: principios para diseñar interfaces efectivas

---

## MÓDULO 15: CLASES ABSTRACTAS, STATIC Y FINAL

**Descripción:** Este módulo profundiza en los modificadores especiales de clases en Java. Las clases abstractas definen plantillas parciales, static se aplica a clases anidadas y miembros, y final protege la integridad del diseño. Aprenderás cuándo y por qué usar cada uno.

1. La palabra abstract para clases
2. Clases abstractas: no se pueden instanciar
3. Métodos abstractos: sin implementación, fuerzan override
4. Miembros abstractos solo en clases abstractas
5. Miembros concretos en clases abstractas
6. Clases abstractas con constructores
7. Constructores en clases abstractas: llamada desde subclase
8. Clases abstractas con métodos concretos
9. Clases abstractas con métodos estáticos
10. Template Method pattern con clases abstractas
11. Clases abstractas vs interfaces: tabla comparativa
12. Cuándo elegir clase abstracta sobre interfaz
13. Cuándo elegir interfaz sobre clase abstracta
14. Heredar de una clase abstracta e implementar interfaces
15. Clase abstracta que implementa interfaz parcialmente
16. Abstract factory pattern
17. Clases abstractas en el framework: AbstractList
18. Clases abstractas en el framework: AbstractMap
19. Clases abstractas en el framework: InputStream
20. Clases abstractas en el framework: OutputStream
21. Clases abstractas en el framework: HttpServlet
22. Clases abstractas en el framework: AbstractController
23. La palabra static para campos
24. Static fields: compartidos entre todas las instancias
25. Static final fields: constantes de clase
26. La palabra static para métodos
27. Static methods: invocados sin instancia
28. Static methods y la keyword this (no permitida)
29. La palabra static para clases anidadas
30. Static nested classes vs inner classes
31. Static nested class no tiene acceso a instancia
32. Static nested class accede a static members de outer
33. Cuándo usar static nested vs inner class
34. Static import: import static java.lang.Math.PI
35. Static import para métodos: import static java.lang.Math.sqrt
36. Bloques estáticos: static { }
37. Múltiples bloques estáticos: se ejecutan en orden
38. Inicialización estática y thread safety
39. Static initialization en clases genéricas
40. Static methods en interfaces (Java 8)
41. Static factory methods como alternativa a constructores
42. List.of(), Map.of(), Set.of() como ejemplos
43. Factory methods: of(), from(), create(), newInstance()
44. Singleton con static method
45. Static inner class como Builder
46. Static methods y testing: difíciles de mockear
47. Evitar static mutable state
48. Dependency injection vs static classes
49. Testing: interfaces para abstraer static calls
50. PowerMock para mockear static (no recomendado)
51. La palabra final para clases
52. final classes: no se puede heredar
53. ¿Por qué final una clase?
54. Performance: final permite devirtualization
55. La JVM optimiza llamadas a métodos de clases final
56. String es una clase final
57. Integer, Long, etc. son clases final
58. Wrapper classes son final
59. La palabra final para métodos
60. final methods: impedir override en subclases
61. final y el error del compilador al intentar override
62. La palabra final para campos
63. final fields: asignables en declaración o constructor
64. final fields y thread safety (safe publication)
65. final parameters: no reasignar parámetros
66. final locals: no reasignar variable local
67. final y el beneficio de inmutabilidad
68. final y el beneficio de legibilidad
69. final como documentación de intención
70. El debate: ¿final por defecto o no?
71. Sealed classes (Java 17)
72. sealed class con permits
73. sealed interface con permits
74. non-sealed: abrir la jerarquía
75. final en subclases de sealed
76. Sealed classes y pattern matching exhaustivo
77. Sealed classes y records
78. Records como final implicit
79. Records y sealed classes combinados
80. Generic classes: clases genéricas
81. Generic class con múltiples parámetros de tipo
82. Bounded type parameters en clases genéricas
83. Default(T) en clases genéricas: null para references, 0 para primitives
84. Static context y generics (type erasure)
85. Static members en clases genéricas (no pueden usar T)
86. Generic singleton pattern
87. Anonymous classes con new Interface() { ... }
88. Anonymous classes y lambdas como alternativa
89. Tuple types: Java no tiene tuplas nativas
90. Record como alternativa a tuplas
91. Record vs clase tradicional
92. Value types vs Reference types resumen
93. Boxing y unboxing: Integer.valueOf(), intValue()
94. Stack vs Heap: dónde viven los objetos
95. GC implications de cada tipo de clase
96. Memory layout de clases en la JVM
97. Type design guidelines de Joshua Bloch
98. Effective Java: Design and Document for Inheritance or Else Prohibit It
99. Prefer composition over inheritance
100. Resumen: reglas para elegir el tipo de clase/modificador correcto

---

## MÓDULO 16: MANEJO DE EXCEPCIONES

**Descripción:** Las excepciones son el mecanismo de Java para manejar errores de forma estructurada. Aprenderás a lanzar, capturar y crear excepciones, la jerarquía de excepciones, checked vs unchecked exceptions, try-with-resources, y las mejores prácticas.

1. ¿Qué es una excepción y por qué existe?
2. Errores de compilación vs errores en runtime
3. Excepciones no controladas (unhandled exceptions)
4. Excepciones controladas (handled exceptions)
5. La sentencia try-catch
6. Múltiples bloques catch para diferentes tipos
7. Multi-catch (Java 7): catch (ExceptionA | ExceptionB e)
8. Jerarquía de excepciones: Throwable
9. Error vs Exception
10. Checked exceptions vs Unchecked exceptions
11. Checked exceptions: el compilador fuerza a capturar o declarar
12. Unchecked exceptions: RuntimeException subclasses
13. Excepciones comunes: NullPointerException
14. Excepciones comunes: ArrayIndexOutOfBoundsException
15. Excepciones comunes: ClassCastException
16. Excepciones comunes: IllegalArgumentException
17. Excepciones comunes: IllegalStateException
18. Excepciones comunes: NumberFormatException
19. Excepciones comunes: ArithmeticException
20. Excepciones comunes: UnsupportedOperationException
21. Excepciones comunes: ConcurrentModificationException
22. Excepciones comunes: StackOverflowError
23. Excepciones comunes: OutOfMemoryError
24. Excepciones comunes: IOException
25. Excepciones comunes: FileNotFoundException
26. Excepciones comunes: SQLException
27. Excepciones comunes: InterruptedException
28. Excepciones comunes: TimeoutException
29. Excepciones comunes: DateTimeException
30. Capturar excepciones específicas primero
31. El bloque catch general: catch (Exception e)
32. El bloque finally
33. try-catch-finally completo
34. try-finally sin catch
35. try-with-resources (Java 7)
36. AutoCloseable y Closeable interfaces
37. Recursos que implementan AutoCloseable
38. Múltiples recursos en try-with-resources
39. Suppressed exceptions en try-with-resources
40. La sentencia throw para lanzar excepciones
41. throw new ExceptionType("message")
42. throws en la declaración del método
43. Propagación de checked exceptions
44. Crear excepciones personalizadas
45. Heredar de Exception para checked exceptions
46. Heredar de RuntimeException para unchecked exceptions
47. Convención: nombre termina en "Exception"
48. Constructor sin parámetros
49. Constructor con mensaje
50. Constructor con mensaje y causa (Throwable cause)
51. Constructor con causa sola
52. Inner exceptions / cause chains
53. getCause() para obtener la causa
54. getMessage() para obtener el mensaje
55. getStackTrace() para obtener el stack trace
56. printStackTrace() para imprimir (evitar en producción)
57. Stack trace y su importancia para debugging
58. fillInStackTrace() para actualizar el stack trace
59. addSuppressed() para excepciones suprimidas
60. getSuppressed() para obtener suprimidas
61. Excepciones en métodos declarados con throws
62. Excepciones en constructores
63. Excepciones en bloques estáticos
64. Excepciones en lambdas
65. Excepciones en streams
66. UncheckedIOException para envolver IOException en lambdas
67. Excepciones en iteradores
68. Excepciones en Comparable/Comparator
69. Evitar catch genérico: catch (Exception e) indiscriminado
70. Cuándo capturar excepciones
71. Cuándo NO capturar excepciones (propagar)
72. Fail fast: detectar errores temprano
73. Exception handling en la capa de presentación
74. Exception handling en la capa de servicio
75. Exception handling en la capa de datos
76. @ExceptionHandler en Spring MVC
77. @ControllerAdvice para manejo global
78. ResponseEntityExceptionHandler
79. ProblemDetail (RFC 7807, Spring 6)
80. Global exception handling en aplicaciones standalone
81. Thread.UncaughtExceptionHandler
82. Operaciones atómicas y rollback en excepciones
83. Patrón compensation para rollback
84. Excepciones vs códigos de error
85. Excepciones vs Optional
86. Excepciones vs Result pattern (no nativo en Java)
87. Vavr Either como alternativa funcional
88. throw en expresiones: Java no tiene throw expressions como Kotlin
89. Depuración: breakpoints en IntelliJ
90. Depuración: step over (F8), step into (F7)
91. Depuración: step out (Shift+F8)
92. Depuración: evaluate expression (Alt+F8)
93. Depuración: watch window
94. Depuración: variables window
95. Depuración: call stack
96. Depuración: conditional breakpoints
97. Depuración: exception breakpoints
98. Depuración: logging breakpoints (sin código)
99. Depuración con System.out.println (quick and dirty)
100. Resumen: reglas de oro para excepciones en Java

---

## MÓDULO 17: COLECCIONES FUNDAMENTALES (JAVA COLLECTIONS FRAMEWORK)

**Descripción:** El Java Collections Framework es una de las bibliotecas más importantes de Java. Aprenderás ArrayList, LinkedList, HashMap, TreeMap, HashSet, TreeSet, Queue, Deque, y las interfaces Collection, List, Set, Map. Entenderás cuándo usar cada colección basándote en el rendimiento y el caso de uso.

1. ¿Qué es el Java Collections Framework?
2. java.util package
3. Interfaces del JCF: Collection, List, Set, Map, Queue, Deque
4. Collection<E>: la interfaz raíz (para List, Set, Queue)
5. Iterable<T>: la interfaz base para for-each
6. List<E>: colección ordenada, permite duplicados
7. ArrayList<E>: implementación basada en array
8. Crear un ArrayList y agregar con add()
9. Acceso por índice: list.get(0)
10. Tamaño: list.size()
11. Insertar en posición con add(index, element)
12. Eliminar con remove(index) y remove(object)
13. Eliminar con removeIf(predicate)
14. Reemplazar con set(index, element)
15. Contener: contains()
16. Índice de: indexOf() y lastIndexOf()
17. SubLista: subList(from, to)
18. Ordenar: Collections.sort() y list.sort()
19. list.sort(Comparator)
20. Comparator.comparing() con lambdas
21. Invertir: Collections.reverse()
22. Mezclar: Collections.shuffle()
23. Copiar: new ArrayList<>(otraLista)
24. List.copyOf() para copia inmutable (Java 10)
25. List.of() para lista inmutable (Java 9)
26. List.of(1, 2, 3)
27. toArray() para convertir a array
28. ArrayList.capacity() y crecimiento automático
29. TrimToSize() para reducir capacidad
30. Rendimiento: ArrayList vs LinkedList
31. LinkedList<E>: implementación basada en nodos enlazados
32. LinkedList como List y como Deque
33. addFirst(), addLast(), getFirst(), getLast()
34. removeFirst(), removeLast()
35. Cuándo usar LinkedList vs ArrayList
36. Vector<E>: legacy, sincronizado, evitar
37. Stack<E>: legacy, usar Deque en su lugar
38. Set<E>: colección sin duplicados
39. HashSet<E>: basado en HashMap (hash table)
40. add(), contains(), remove()
41. No permite duplicados: add() retorna false
42. No garantiza orden
43. Rendimiento: O(1) para add, contains, remove
44. LinkedHashSet<E>: mantiene orden de inserción
45. TreeSet<E>: basado en TreeMap (árbol rojo-negro)
46. TreeSet: elementos ordenados
47. TreeSet requiere Comparable o Comparator
48. NavigableSet: first(), last(), lower(), higher()
49. SortedSet: headSet(), tailSet(), subSet()
50. EnumSet<E>: optimizado para enums
51. Set.of() para conjunto inmutable (Java 9)
52. Operaciones de conjuntos con Sets
53. Unión: manual con addAll()
54. Intersección: manual con retainAll()
55. Diferencia: manual con removeAll()
56. Guava Sets.union(), Sets.intersection()
57. Map<K, V>: asociación clave-valor
58. HashMap<K, V>: basado en hash table
59. put(key, value), get(key)
60. getOrDefault(key, defaultValue)
61. putIfAbsent(key, value)
62. containsKey() y containsValue()
63. remove(key), remove(key, value)
64. replace(key, value), replace(key, oldVal, newVal)
65. size(), isEmpty()
66. keySet(), values(), entrySet()
67. Iterar con entrySet() y for-each
68. Iterar con forEach() (Java 8)
69. compute(), computeIfAbsent(), computeIfPresent()
70. merge() para combinar valores
71. get() retorna null si no existe la clave
72. Rendimiento: O(1) promedio para get y put
73. Hashing: hashCode() y equals()
74. El contrato entre hashCode() y equals()
75. Buenas prácticas para hashCode()
76. Collision handling en HashMap
77. Load factor y rehashing
78. LinkedHashMap<K, V>: mantiene orden de inserción
79. LinkedHashMap con access-order (LRU cache)
80. TreeMap<K, V>: basado en red-black tree
81. TreeMap: claves ordenadas
82. TreeMap requiere Comparable o Comparator
83. NavigableMap: firstKey(), lastKey(), lowerKey()
84. SortedMap: headMap(), tailMap(), subMap()
85. EnumMap<K, V>: optimizado para enums con keys enum
86. WeakHashMap: keys como weak references
87. IdentityHashMap: usa == en vez de equals()
88. Hashtable: legacy, sincronizado, evitar
89. Properties: hashtable para configuración
90. Map.of() para mapa inmutable (Java 9)
91. Map.ofEntries() para mapas con más de 10 entradas
92. Map.entry() para crear entradas
93. Queue<E>: primero en entrar, primero en salir (FIFO)
94. PriorityQueue<E>: cola de prioridad
95. PriorityQueue con Comparator personalizado
96. offer(), poll(), peek()
97. Deque<E): doble extremo (double-ended queue)
98. ArrayDeque<E>: implementación de Deque
99. offerFirst(), offerLast(), pollFirst(), pollLast()
100. Resumen: tabla de selección de colección

---

## MÓDULO 18: COLECCIONES AVANZADAS Y CONCURRENTES

**Descripción:** Más allá de las colecciones fundamentales, Java ofrece colecciones para situaciones especiales: colecciones inmutables, colecciones concurrentes, colecciones observables, y utilidades de colecciones. Este módulo te prepara para programación concurrente y arquitecturas robustas.

1. java.util.concurrent package
2. ConcurrentHashMap<K, V>
3. ConcurrentHashMap: put(), get(), remove()
4. ConcurrentHashMap: putIfAbsent(), compute()
5. ConcurrentHashMap: thread-safe sin sincronizar todo el mapa
6. ConcurrentHashMap vs Hashtable vs Collections.synchronizedMap()
7. ConcurrentLinkedQueue<E>: cola concurrente lock-free
8. ConcurrentLinkedDeque<E>: deque concurrente lock-free
9. CopyOnWriteArrayList<E>
10. CopyOnWriteArrayList: thread-safe para reads frecuentes
11. CopyOnWriteArrayList: copy-on-write en modificaciones
12. CopyOnWriteArraySet<E>
13. BlockingQueue<E>: cola con operaciones bloqueantes
14. ArrayBlockingQueue: bounded, array-based
15. LinkedBlockingQueue: optional bounded, linked-based
16. PriorityBlockingQueue: cola de prioridad bloqueante
17. SynchronousQueue: sin capacidad, direct handoff
18. DelayQueue: elementos disponibles después de un delay
19. LinkedTransferQueue: transfer elements
20. put() y take() como operaciones bloqueantes
21. offer() y poll() con timeout
22. Producer-Consumer pattern con BlockingQueue
23. ConcurrentSkipListMap<K, V>: sorted concurrent map
24. ConcurrentSkipListSet<E>: sorted concurrent set
25. Collections.synchronizedList() wrapper
26. Collections.synchronizedMap() wrapper
27. Collections.synchronizedSet() wrapper
28. Collections.unmodifiableList() wrapper
29. Collections.unmodifiableMap() wrapper
30. Collections.unmodifiableSet() wrapper
31. Collections.unmodifiableCollection()
32. List.of(), Set.of(), Map.of() como alternativas inmutables
33. List.copyOf(), Set.copyOf(), Map.copyOf() (Java 10)
34. EnumSet y EnumMap como colecciones eficientes para enums
35. EnumSet.allOf(), of(), range()
36. Guava ImmutableList, ImmutableMap, ImmutableSet
37. Guava Lists, Maps, Sets utilities
38. Guava Multimap, Multiset
39. Guava Table (mapa bidimensional)
40. Guava ImmutableListMultimap
41. Apache Commons Collections
42. Bag, BidiMap, OrderedMap
43. Custom collections: implementar Collection<E>
44. Implementar List<E> personalizado
45. Implementar Set<E> personalizado
46. Implementar Map<K,V> personalizado
47. Iterator personalizado con remove()
48. Spliterator para iteración paralela
49. Iterable<T> con iterator() personalizado
50. Iterable con streams: stream(), parallelStream()
51. Lazy evaluation con Spliterator
52. Thread-safe collections: guía de uso
53. Lock-free collections vs lock-based
54. compareAndSet (CAS) en colecciones concurrentes
55. java.util.SequencedCollection (Java 21)
56. SequencedCollection: addFirst(), addLast()
57. SequencedCollection: getFirst(), getLast()
58. SequencedCollection: reversed()
59. SequencedSet y SequencedMap (Java 21)
60. LinkedHashMap como SequencedMap
61. TreeMap como SequencedMap
62. Comparadores personalizados con Comparator<T>
63. Comparator.comparing() con lambda
64. Comparator.thenComparing() para ordenamiento múltiple
65. Comparator.reversed() para invertir
66. Comparator.naturalOrder() y reverseOrder()
67. Comparator.nullsFirst() y nullsLast()
68. Collections.frequency() para contar elementos
69. Collections.disjoint() para verificar intersección
70. Collections.indexOfSubList()
71. Collections.rotate() para rotar elementos
72. Collections.swap() para intercambiar
73. Collections.fill() para llenar
74. Collections.replaceAll()
75. Collections.min() y Collections.max()
76. Collections.binarySearch() en listas ordenadas
77. PriorityQueue y casos de uso (Dijkstra, scheduling)
78. TreeMap y NavigableMap para rangos
79. headMap(), tailMap(), subMap() para rangos de claves
80. Rendimiento de operaciones en colecciones
81. Capacity y resizing en ArrayList y HashMap
82. Preallocar capacidad con constructor
83. Memory footprint de diferentes colecciones
84. HashSet vs TreeSet vs LinkedHashSet: benchmark
85. HashMap vs TreeMap vs LinkedHashMap: benchmark
86. Colecciones y serialización (Serializable)
87. Colecciones y JSON (Jackson, Gson)
88. Collections con generics avanzado
89. Wildcard types con colecciones
90. PECS: Producer Extends, Consumer Super
91. Collections.checkedList() para type safety en runtime
92. Collections.singleton() para colección de un elemento
93. Collections.emptyList() como alternativa a null
94. Collections.emptyMap() y emptySet()
95. NavigableSet y NavigableMap: operaciones de navegación
96. descendingIterator(), descendingSet()
97. floor(), ceiling(), lower(), higher()
98. pollFirst(), pollLast()
99. Colecciones como backing de clases
100. Resumen: tabla avanzada de selección de colección

---

## MÓDULO 19: GENÉRICOS (GENERICS)

**Descripción:** Los genéricos permiten escribir código reutilizable y type-safe. Aprenderás a crear clases, métodos, interfaces con genéricos, a usar bounded type parameters, a entender la varianza con wildcards, y los aspectos de type erasure.

1. ¿Qué son los genéricos y por qué son necesarios?
2. El problema de usar Object: casting, sin type safety
3. List<E> como ejemplo fundamental de genérico
4. Crear métodos genéricos
5. Inferencia de tipo en llamadas a métodos genéricos
6. Múltiples parámetros de tipo: <K, V>
7. Naming conventions: E (element), K (key), V (value), T (type), R (result)
8. Crear clases genéricas
9. Crear interfaces genéricas
10. Genéricos y null: T puede ser null para referencias
11. Genéricos con tipos primitivos: autoboxing automático
12. No se puede new T(): type erasure
13. No se puede new T[]: workarounds
14. Bounded type parameters: <T extends Comparable<T>>
15. <T extends Number>: tipo debe ser Number o subclase
16. <T extends Comparable<T>>: tipo debe implementar Comparable
17. Multiple bounds: <T extends Comparable<T> & Serializable>
18. & para múltiples bounds (primero clase, luego interfaces)
19. Wildcards: <?> (unbounded wildcard)
20. <? extends T> (upper bounded wildcard)
21. <? super T> (lower bounded wildcard)
22. PECS: Producer Extends, Consumer Super
23. Producer: <? extends T> solo lee
24. Consumer: <? super T> solo escribe
25. Wildcard capture
26. Raw types: List sin tipo (evitar)
27. Raw types y backwards compatibility
28. Type erasure: cómo funciona
29. Los genéricos se borran en runtime
30. List<String> y List<Integer> son el mismo tipo en runtime
31. Consecuencias de type erasure
32. No se puede verificar instanceof con genéricos
33. No se puede crear arrays de genéricos
34. Workarounds: Class<T> como token
35. @SuppressWarnings("unchecked") para casting genérico seguro
36. Type erasure y herencia
37. Generic methods con bounded wildcards
38. Collections.sort(List<T>) con Comparable
39. Collections.max(Collection<? extends T>)
40. Collections.copy(List<? super T>, List<? extends T>)
41. List.addAll(Collection<? extends E>)
42. Genéricos y constructores
43. Static members en clases genéricas (no pueden usar T)
44. Cada instanciación de tipo comparte la misma clase
45. Singleton genérico: no es posible directamente
46. Genéricos y reflexión: getGenericType()
47. ParameterizedType, GenericArrayType, WildcardType
48. TypeVariable para obtener parámetros de tipo
49. Generics en runtime con reflection
50. @FunctionalInterface con genéricos
51. Function<T, R> como genérico funcional
52. BiFunction<T, U, R>
53. Predicate<T> como genérico
54. Consumer<T> y Supplier<T>
55. UnaryOperator<T> y BinaryOperator<T>
56. Genéricos y Optional<T>
57. Optional<T> como wrapper nullable
58. Genéricos y Stream<T>
59. Stream<T> methods con wildcards
60. Stream.of(T... values)
61. Genéricos y CompletableFuture<T>
62. Generic Repository pattern
63. Generic Service pattern
64. Generic Factory pattern
65. Generic Builder pattern
66. Generic extension methods: no existen en Java
67. Generic comparable: Comparable<T>
68. Self-referencing generics: Comparable<T> en T
69. Recursive type bounds: <T extends Comparable<T>>
70. Generic enum: no se puede (enums no son genéricos)
71. Generic exceptions: no se puede (exceptions no son genéricas)
72. Genéricos y serialización
73. Genéricos y JSON (Jackson TypeReference)
74. ObjectMapper.getTypeFactory().constructParametricType()
75. Genéricos y JDBC
76. Genéricos y Dependency Injection (Spring)
77. Genéricos y JPA: JpaRepository<T, ID>
78. Genéricos y Unit Testing
79. Mockito y genéricos
80. Genéricos y CompletableFuture<T>
81. Supplier<T> y genéricos
82. Generic converters
83. Generic validators
84. Generic comparers
85. Type-safe heterogeneous containers
86. Class<T> como key para type-safe containers
87. Generics y lombok @Builder
88. Genéricos y records
89. record Pair<A, B>(A first, B second)
90. Genéricos y sealed classes
91. Anti-patterns: over-abstraction con genéricos
92. Cuándo NO usar genéricos
93. Java generics vs C# generics: diferencias fundamentales
94. Reified generics (no existen en Java)
95. Project Valhalla y specialized generics (futuro)
96. Wildcard capture helper methods
97. Intersection types con bounds
98. Generics y covarianza/contravarianza
99. Arrays son covariantes, generics son invarianes
100. Resumen: principios para diseño genérico efectivo

---

## MÓDULO 20: LAMBDAS, INTERFACES FUNCIONALES Y METHOD REFERENCES

**Descripción:** Las lambdas (Java 8) transformaron Java de un lenguaje verboso a uno conciso. Aprenderás expresiones lambda, interfaces funcionales, method references, y cómo se integran con el Collections Framework. Este es el módulo que moderniza tu Java.

1. ¿Qué son las lambdas y por qué llegaron a Java?
2. Java antes de lambdas: anonymous inner classes
3. Sintaxis de lambda: (params) -> expression
4. Lambda con un parámetro: x -> x * 2
5. Lambda con múltiples parámetros: (x, y) -> x + y
6. Lambda sin parámetros: () -> System.out.println("hola")
7. Lambda con cuerpo de bloque: (x) -> { return x + 1; }
8. Lambda con cuerpo de expresión: x -> x + 1
9. Inferencia de tipos en lambdas
10. Tipado explícito en lambdas: (int x, int y) -> x + y
11. @FunctionalInterface annotation
12. ¿Qué es una interfaz funcional?
13. Una interfaz con exactamente un método abstracto
14. Default methods no cuentan como abstractos
15. Static methods no cuentan como abstractos
16. java.util.function package
17. Function<T, R>: acepta T, retorna R
18. BiFunction<T, U, R>: acepta T y U, retorna R
19. Predicate<T>: acepta T, retorna boolean
20. BiPredicate<T, U>: acepta T y U, retorna boolean
21. Consumer<T>: acepta T, no retorna nada (void)
22. BiConsumer<T, U>: acepta T y U, no retorna nada
23. Supplier<T>: no acepta nada, retorna T
24. UnaryOperator<T>: acepta T, retorna T (extends Function)
25. BinaryOperator<T>: acepta T y T, retorna T
26. IntFunction, LongFunction, DoubleFunction
27. IntPredicate, LongPredicate, DoublePredicate
28. IntConsumer, LongConsumer, DoubleConsumer
29. IntSupplier, LongSupplier, DoubleSupplier
30. ToIntFunction<T>, ToLongFunction<T>
31. Comparar con delegados de C#: Action, Func, Predicate
32. Lambdas asignadas a variables de tipo funcional
33. Lambdas como argumentos de métodos
34. Lambdas en Collections.sort() con Comparator
35. Lambdas en list.forEach()
36. Lambdas en list.removeIf()
37. Lambdas en Map.forEach()
38. Lambdas en streams: filter, map, reduce
39. Method references: ClassName::methodName
40. Referencia a método estático: Math::abs
41. Referencia a método de instancia de un objeto: System.out::println
42. Referencia a método de instancia de un tipo: String::length
43. Referencia a constructor: ArrayList::new
44. Referencia a constructor de array: String[]::new
45. Cuándo usar method reference vs lambda
46. Closures: captura de variables en lambdas
47. Variables capturadas deben ser effectively final
48. effectively final: no se reasigna después de inicializar
49. Closures y la regla de effectively final
50. Closures y thread safety
51. Lambdas y excepciones checked
52. No se puede throw checked exception en lambda de Function
53. Workarounds: wrapper con RuntimeException
54. Sneaky throws (no recomendado)
55. Functional interfaces que lanzan checked exceptions
56. Vavr's Try como alternativa
57. Lambdas recursivas
58. Lambdas y memoization
59. Lambdas y composición: andThen(), compose()
60. Function.andThen(Function) y Function.compose(Function)
61. Predicate.and(), Predicate.or(), Predicate.negate()
62. Consumer.andThen(Consumer)
63. BinaryOperator.minBy() y maxBy()
64. Patrones con lambdas: Strategy
65. Patrones con lambdas: Command
66. Patrones con lambdas: Observer
67. Patrones con lambdas: Callback
68. Patrones con lambdas: Dependency Injection
69. Lambdas y Comparator
70. Comparator.comparing(Function)
71. Comparator.thenComparing()
72. Comparator.reversed()
73. Comparator.nullsFirst() y nullsLast()
74. Lambdas y Optional
75. Optional.map(), filter(), flatMap()
76. Optional.ifPresent(), ifPresentOrElse()
77. Lambdas y Streams (introducción, M21 profundiza)
78. stream().filter(x -> x > 5)
79. stream().map(x -> x * 2)
80. stream().reduce(0, (a, b) -> a + b)
81. Anonymous classes vs lambdas
82. Diferencias: this, shadowing, scope
83. En lambdas, this se refiere a la clase contenedora
84. En anonymous classes, this se refiere a la anonymous class
85. Performance de lambdas: invokedynamic
86. LambdaMetafactory y bootstrap methods
87. Lambda allocation: heap vs singleton
88. Singleton lambdas (sin captura)
89. Non-capturing vs capturing lambdas
90. Lambdas y serialización
91. Serialized lambdas (raramente usado)
92. Lambdas en event handling (Swing, JavaFX)
93. ActionListener con lambda: e -> doSomething()
94. Lambdas y Spring: @EventListener con lambdas
95. Lambdas y testing: fácil de crear
96. Lambdas en assertions
97. Lambdas y JUnit 5: assertThrows(() -> ...)
98. Mockito.verify() con ArgumentMatcher lambda
99. Anti-patterns: lambdas demasiado largas
100. Resumen: cuándo usar lambdas, method references y anonymous classes

---

## MÓDULO 21: STREAMS API Y OPTIONAL

**Descripción:** La Streams API (Java 8) es una de las características más poderosas de Java moderno, permitiendo procesar colecciones de forma declarativa y funcional. Optional elimina NullPointerExceptions explícitos. Aprenderás operaciones intermedias y terminales, paralelización, y patrones funcionales.

1. ¿Qué es la Streams API y por qué es revolucionaria?
2. java.util.stream package
3. Stream<T>: flujo de datos procesable
4. Crear streams: collection.stream()
5. Crear streams: Stream.of(), Stream.empty()
6. Crear streams: Stream.iterate()
7. Crear streams: Stream.generate()
8. Crear streams: Arrays.stream(array)
9. Crear streams: Files.lines(path)
10. Crear streams: IntStream.range() y rangeClosed()
11. Crear streams: Stream.builder()
12. Operaciones intermedias: lazy (no ejecutan hasta terminal)
13. Operaciones terminales: ejecutan el pipeline
14. filter(Predicate) para filtrar
15. map(Function) para transformar
16. flatMap(Function) para aplanar
17. sorted() para ordenar
18. sorted(Comparator) con comparador
19. distinct() para eliminar duplicados
20. limit(n) para limitar elementos
21. skip(n) para saltar elementos
22. peek(Consumer) para observar sin modificar
23. takeWhile(Predicate) (Java 9)
24. dropWhile(Predicate) (Java 9)
25. Terminal: forEach(Consumer)
26. Terminal: collect(Collector)
27. Terminal: reduce(BinaryOperator)
28. Terminal: reduce(identity, BinaryOperator)
29. Terminal: count()
30. Terminal: anyMatch(Predicate)
31. Terminal: allMatch(Predicate)
32. Terminal: noneMatch(Predicate)
33. Terminal: findFirst()
34. Terminal: findAny()
35. Terminal: min(Comparator) y max(Comparator)
36. Terminal: toArray()
37. Terminal: forEachOrdered() para orden en paralelo
38. Collectors.toList() para List
39. Collectors.toSet() para Set
40. Collectors.toMap() para Map
41. Collectors.toMap() con merge function
42. Collectors.joining() para concatenar strings
43. Collectors.joining(", ")
44. Collectors.counting()
45. Collectors.summingInt(), summingDouble()
46. Collectors.averagingInt(), averagingDouble()
47. Collectors.groupingBy(Function)
48. Collectors.groupingBy con downstream collector
49. Collectors.partitioningBy(Predicate)
50. Collectors.toUnmodifiableList() (Java 10)
51. Collectors.toUnmodifiableSet() (Java 10)
52. Collectors.toUnmodifiableMap() (Java 10)
53. Collectors.collectingAndThen()
54. Collectors.flatMapping() (Java 9)
55. Collectors.filtering() (Java 9)
56. Collectors.teeing() (Java 12)
57. Streams con tipos primitivos: IntStream, LongStream, DoubleStream
58. IntStream.range(1, 100)
59. IntStream.sum(), average(), min(), max()
60. IntStream.summaryStatistics()
61. boxed() para convertir IntStream a Stream<Integer>
62. mapToInt(), mapToLong(), mapToDouble()
63. flatMapToInt(), flatMapToLong()
64. Parallel streams: .parallel() o .parallelStream()
65. Cuándo usar parallel streams
66. Parallel streams y thread safety
67. Parallel streams: evitar side effects
68. Ordered streams y parallel performance
69. Streams son single-use: no reutilizables
70. IllegalStateException al reusar stream
71. Streams y excepciones
72. try-catch dentro de lambdas
73. UncheckedIOException para IOException
74. Streams con Optional
75. stream().findFirst() retorna Optional<T>
76. stream().max() retorna Optional<T>
77. Optional.orElse() para valor por defecto
78. Optional.orElseThrow()
79. Optional.orElseGet(Supplier)
80. Optional: ¿Qué es y por qué existe?
81. Optional.of(value) para valor no null
82. Optional.empty() para vacío
83. Optional.ofNullable(value) para posiblemente null
84. Optional.isPresent() y Optional.isEmpty()
85. Optional.ifPresent(Consumer)
86. Optional.ifPresentOrElse(Consumer, Runnable) (Java 9)
87. Optional.map(Function) para transformar
88. Optional.flatMap(Function) para aplanar
89. Optional.filter(Predicate) para filtrar
90. Optional.or(Supplier<Optional<T>>) (Java 9)
91. Optional.stream() (Java 9)
92. Optional.orElseThrow() sin argumentos (Java 10)
93. Cuándo usar Optional: retorno de métodos
94. No usar Optional en parámetros
95. No usar Optional en campos
96. Optional y streams: optional.stream()
97. Empty streams: Stream.empty()
98. Stream.ofNullable() (Java 9)
99. Streams inmutable con toUnmodifiableList()
100. Resumen: tabla completa de operadores de Stream

---

## MÓDULO 22: CONCURRENCIA Y MULTITHREADING

**Descripción:** Java tiene uno de los modelos de concurrencia más robustos. Aprenderás threads, executors, CompletableFuture, sincronización, concurrent collections, y los virtual threads de Java 21. Este módulo es esencial para construir aplicaciones de alto rendimiento.

1. ¿Qué es concurrencia y por qué es necesaria?
2. Concurrencia vs paralelismo
3. Threads en Java: la clase Thread
4. Crear un thread: heredar de Thread
5. Crear un thread: implementar Runnable
6. Thread.start() y Thread.run()
7. Thread.sleep() para pausar
8. Thread.join() para esperar a que termine
9. Thread.interrupt() e InterruptedException
10. Thread.isAlive() y Thread.getState()
11. Thread States: NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED
12. Thread naming para debugging
13. Daemon threads: Thread.setDaemon(true)
14. Thread priorities: setPriority()
15. Race conditions: qué son y cómo ocurren
16. El operador synchronized
17. Synchronized methods
18. Synchronized blocks
19. Intrinsic locks (monitor locks)
20. Deadlocks: qué son y cómo prevenirlos
21. Livelock y starvation
22. La palabra volatile
23. volatile garantiza visibilidad pero no atomicidad
24. Atomic classes: AtomicInteger, AtomicLong, AtomicBoolean
25. AtomicInteger: incrementAndGet(), compareAndSet()
26. AtomicReference<V> para referencias atómicas
27. AtomicStampedReference para ABA problem
28. LongAdder y LongAccumulator (mejor que AtomicLong para contendencia alta)
29. java.util.concurrent.locks package
30. ReentrantLock
31. lock() y unlock()
32. tryLock() con timeout
33. lockInterruptibly()
34. ReentrantReadWriteLock
35. StampedLock (Java 8)
36. Condition con Lock: await() y signal()
37. Semaphore para limitar concurrencia
38. Semaphore.acquire() y release()
39. CountDownLatch para esperar N eventos
40. CyclicBarrier para sincronizar N threads
41. Phaser como alternativa flexible a CyclicBarrier y CountDownLatch
42. Exchanger para intercambiar datos entre 2 threads
43. ExecutorService para gestión de threads
44. Executors.newFixedThreadPool(n)
45. Executors.newCachedThreadPool()
46. Executors.newSingleThreadExecutor()
47. Executors.newScheduledThreadPool(n)
48. execute(Runnable) para tareas sin retorno
49. submit(Callable<T>) para tareas con retorno
50. Future<T> para resultado futuro
51. future.get() para obtener resultado (bloqueante)
52. future.get(timeout, unit) con timeout
53. future.cancel() y future.isCancelled()
54. future.isDone()
55. invokeAll() y invokeAny()
56. CompletableFuture<T> (Java 8)
57. CompletableFuture.supplyAsync(Supplier)
58. CompletableFuture.runAsync(Runnable)
59. thenApply(Function) para transformar
60. thenAccept(Consumer) para consumir
61. thenRun(Runnable) para ejecutar después
62. thenCompose() para encadenar (flatMap)
63. thenCombine() para combinar dos futures
64. allOf() y anyOf() para múltiples futures
65. exceptionally(Function) para manejo de errores
66. handle(BiFunction) para manejo siempre
67. complete() y completeExceptionally()
68. CompletableFuture y Executor personalizado
69. Virtual Threads (Java 21)
70. Thread.ofVirtual().start(() -> {})
71. Thread.startVirtualThread(() -> {})
72. Executors.newVirtualThreadPerTaskExecutor()
73. Virtual threads: ligeros, muchos concurrentes
74. Virtual threads vs platform threads
75. Pinned virtual threads
76. Structured Concurrency (Preview, Java 21)
77. StructuredTaskScope.ShutdownOnFailure
78. StructuredTaskScope.ShutdownOnSuccess
79. Scoped Values (Preview, Java 21)
80. ScopedValues como alternativa a ThreadLocal
81. ThreadLocal<T> para datos por thread
82. ThreadLocal.withInitial(Supplier)
83. InheritableThreadLocal<T>
84. ThreadLocal y memory leaks
85. ForkJoinPool y work-stealing
86. RecursiveTask<V> y RecursiveAction
87. ForkJoinPool.commonPool()
88. Parallel streams usan ForkJoinPool
89. CompletableFuture y ForkJoinPool
90. Phaser como reemplazo avanzado de CyclicBarrier
91. Testing concurrent code
92. Stress testing con ExecutorService
93. Detectar deadlocks: ThreadMXBean
94. jstack para analizar threads
95. jconsole para monitorear threads
96. Java Flight Recorder para profiling
97. ConcurrentHashMap (revisión desde M18)
98. Concurrent collections internals
99. Thread-safe patterns: immutable objects
100. Resumen: guía de selección de mecanismo de concurrencia

---

## MÓDULO 23: E/S (I/O) Y NIO

**Descripción:** Cualquier aplicación real necesita interactuar con el sistema de archivos y red. Aprenderás java.io (streams, readers/writers), java.nio (channels, buffers), java.nio.file (Files, Path), y las APIs modernas de I/O de Java.

1. java.io package: overview
2. InputStream y OutputStream: streams de bytes
3. FileInputStream para leer archivos de bytes
4. FileOutputStream para escribir archivos de bytes
5. BufferedInputStream y BufferedOutputStream
6. DataInputStream y DataOutputStream
7. PrintStream para imprimir (System.out es PrintStream)
8. Reader y Writer: streams de caracteres
9. FileReader y FileWriter
10. BufferedReader y BufferedWriter
11. BufferedReader.readLine() para leer líneas
12. PrintWriter para escribir texto
13. InputStreamReader: puente de bytes a caracteres
14. OutputStreamWriter: puente de caracteres a bytes
15. try-with-resources para cerrar streams automáticamente
16. AutoCloseable e Closeable
17. ByteArrayOutputStream para escribir en memoria
18. ByteArrayInputStream para leer de memoria
19. PipedInputStream y PipedOutputStream
20. SequenceInputStream para concatenar streams
21. PushbackInputStream para "devolver" bytes
22. java.nio.file package (NIO.2, Java 7)
23. Path: representar rutas de archivos
24. Paths.get("/home/user/file.txt")
25. Path.of() (Java 11)
26. Path: resolve(), relativize(), normalize()
27. Path: getFileName(), getParent(), getRoot()
28. Path: toAbsolutePath(), toRealPath()
29. Path: isAbsolute(), startsWith(), endsWith()
30. Files: operaciones con archivos y directorios
31. Files.readString(path) (Java 11)
32. Files.writeString(path, content) (Java 11)
33. Files.readAllLines(path)
34. Files.readAllBytes(path)
35. Files.write(path, lines) y Files.write(path, bytes)
36. Files.exists(path) y Files.notExists(path)
37. Files.createFile(path) y Files.createDirectory(path)
38. Files.createDirectories(path) para crear árbol
39. Files.delete(path) y Files.deleteIfExists(path)
40. Files.copy(source, target)
41. Files.move(source, target)
42. Files.size(path) y Files.getLastModifiedTime()
43. Files.setAttribute() y Files.getAttribute()
44. Files.isHidden() y Files.isSymbolicLink()
45. Files.walk(path) para recorrer recursivamente
46. Files.list(path) para listar directorio
47. Files.find() para buscar con filtro
48. Files.lines(path) como Stream<String>
49. Files.newBufferedReader() y Files.newBufferedWriter()
50. Files.newInputStream() y Files.newOutputStream()
51. FileSystem y FileSystems.getDefault()
52. FileVisitor para visitar archivos recursivamente
53. SimpleFileVisitor como implementación base
54. FileVisitResult: CONTINUE, TERMINATE, SKIP_SUBTREE
55. WatchService para monitorear cambios en archivos
56. WatchKey y WatchEvent
57. IN_CREATE, IN_MODIFY, IN_DELETE events
58. Glob patterns para filtrar archivos
59. DirectoryStream con filtros
60. FileStore para información de discos
61. FileAttribute para permisos
62. PosixFilePermissions en Linux
63. java.nio.channels: Channels y Buffers
64. ByteBuffer para buffers de bytes
65. CharBuffer para buffers de caracteres
66. IntBuffer, LongBuffer, DoubleBuffer
67. Buffer: position, limit, capacity
68. Buffer.flip(), clear(), rewind(), compact()
69. FileChannel para I/O de archivos con channels
70. FileChannel.read(ByteBuffer)
71. FileChannel.write(ByteBuffer)
72. FileChannel.transferTo() y transferFrom()
73. Memory-mapped files con FileChannel.map()
74. MappedByteBuffer
75. SocketChannel para I/O de red
76. ServerSocketChannel para servidores
77. Selector para I/O multiplexado
78. Selector.select() para monitorear múltiples channels
79. Non-blocking I/O con channels
80. java.nio.charset: Charset, CharsetEncoder, CharsetDecoder
81. StandardCharsets.UTF_8
82. Files.readString con charset (Java 11)
83. java.util.Scanner para leer input
84. Scanner.nextInt(), nextLine(), nextDouble()
85. java.io.Console para I/O de consola
86. System.console() para acceso a consola
87. Temporary files: Files.createTempFile()
88. Temporary directories: Files.createTempDirectory()
89. File locking: FileChannel.lock()
90. File locking: FileChannel.tryLock()
91. RandomAccessFile para acceso aleatorio
92. RandomAccessFile.seek() y read/write
93. Large file processing: streaming vs loading all
94. Line-by-line processing con BufferedReader
95. Line-by-line processing con Files.lines()
96. Large file processing con channels
97. File hashing: MessageDigest con streams
98. File encoding: UTF-8, UTF-16, BOM
99. Cross-platform paths con Path.of()
100. Resumen: mejores prácticas para I/O en Java

---

## MÓDULO 24: SERIALIZACIÓN (JSON, XML, BINARIO)

**Descripción:** La serialización convierte objetos en formatos transportables. Aprenderás JSON con Jackson y Gson, XML con JAXB y dom4j, y serialización binaria nativa de Java. Cada formato tiene sus casos de uso.

1. ¿Qué es serialización y deserialización?
2. Tipos de serialización: JSON, XML, Binary
3. Serializable interface en Java
4. serialVersionUID para control de versiones
5. transient keyword para excluir campos
6. ObjectInputStream y ObjectOutputStream
7. Serializar/deserializar con streams
8. Externalizable como alternativa a Serializable
9. readExternal() y writeExternal()
10. Los riesgos de la serialización nativa de Java
11. Vulnerabilidades de deserialización (CVEs)
12. Alternativas: JSON y XML como formatos seguros
13. Jackson: el serializador JSON más usado en Java
14. ObjectMapper: el corazón de Jackson
15. objectMapper.writeValueAsString(obj)
16. objectMapper.readValue(json, Class)
17. @JsonProperty para nombres personalizados
18. @JsonIgnore para excluir campos
19. @JsonIgnoreProperties para excluir múltiples
20. @JsonInclude(Include.NON_NULL)
21. @JsonFormat para formato de fechas
22. @JsonCreator para constructores personalizados
23. @JsonSetter para setters personalizados
24. @JsonGetter para getters personalizados
25. @JsonTypeInfo para polimorfismo
26. @JsonSubTypes para subtipos
27. SerializationFeature.INDENT_OUTPUT
28. DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES
29. ObjectMapper.configure()
30. ObjectMapper.registerModule()
31. JavaTimeModule para java.time types
32. Jackson y records (Java 16+)
33. JsonNode para navegación sin tipo
34. ObjectNode, ArrayNode, TextNode
35. JsonNode.get("field"), asText(), asInt()
36. Jackson streaming API: JsonParser, JsonGenerator
37. TypeReference<T> para tipos genéricos
38. ObjectMapper.getTypeFactory()
39. Jackson annotations avanzadas
40. @JsonView para vistas de serialización
41. @JsonManagedReference y @JsonBackReference
42. @JsonIdentityInfo para referencias circulares
43. Jackson custom serializers/deserializers
44. JsonSerializer<T> y JsonDeserializer<T>
45. Gson: alternativa ligera de Google
46. Gson gson = new Gson()
47. gson.toJson(obj) y gson.fromJson(json, Class)
48. @SerializedName para nombres personalizados
49. @Expose para control de exposición
50. GsonBuilder para configuración
51. JsonParser de Gson para parsing manual
52. Gson y tipos genéricos: TypeToken
53. Moshi como alternativa moderna de Square
54. Moshi: más simple y con Kotlin support
55. JSON-B (Jakarta JSON Binding): estándar
56. @JsonbProperty, @JsonbNillable
57. XML serialization con JAXB
58. @XmlRootElement, @XmlElement, @XmlAttribute
59. @XmlAccessorType
60. Marshaller y Unmarshaller
61. JAXBContext.newInstance()
62. Jakarta XML Binding (migración de javax)
63. dom4j para XML parsing
64. DocumentBuilder y DocumentBuilderFactory
65. DOM parsing: carga todo en memoria
66. SAX parsing: event-driven, no carga todo
67. StAX parsing: pull-based
68. XPath para consultas XML
69. XSLT para transformación de XML
70. Protocol Buffers con protobuf-java
71. MessagePack para Java
72. Apache Avro
73. Kryo para serialización binaria rápida
74. JSON en Spring Boot: auto-configuración con Jackson
75. @RequestBody y @ResponseBody
76. ResponseEntity<T> y JSON
77. RestTemplate con JSON
78. WebClient con JSON
79. JSON y JPA entities: evitar lazy loading
80. DTOs para JSON serialization
81. ModelMapper para mapeo
82. MapStruct para mapeo compile-time
83. JSON Schema validation
84. JSON Patch (RFC 6902)
85. JSON Merge Patch
86. JSON Lines format
87. Testing serialization: round-trip tests
88. Serialization benchmarks: Jackson vs Gson vs Moshi
89. JSON y virtual threads (Java 21)
90. JSON en gRPC: transcoding
91. JSON en Kafka: serdes
92. JSON en MongoDB
93. JSON en Redis
94. JSON en Elasticsearch
95. JSON en configuración: application.properties/YAML
96. JSON en testing: fixtures
97. JSON y null safety
98. JSON y records: serialización de records
99. JSON y sealed classes
100. Resumen: guía de selección de formato y serializador

---

## MÓDULO 25: EXPRESIONES REGULARES

**Descripción:** Las expresiones regulares (regex) son herramientas poderosas para búsqueda y manipulación de patrones en texto. Aprenderás java.util.regex, la clase Pattern y Matcher, y cómo usarlas para validación, extracción y reemplazo de texto.

1. ¿Qué son las expresiones regulares?
2. java.util.regex package
3. Pattern.compile(regex) para compilar un patrón
4. Pattern.matches(regex, input) para verificación rápida
5. Matcher para búsquedas detalladas
6. pattern.matcher(input) para crear Matcher
7. matcher.find() para buscar la siguiente coincidencia
8. matcher.matches() para verificar coincidencia completa
9. matcher.group() para obtener la coincidencia
10. matcher.start() y matcher.end() para posiciones
11. Caracteres literales en regex
12. Metacaracteres: . * + ? ^ $ | \ [ ] ( ) { }
13. El punto (.) como wildcard de un carácter
14. Cuantificador * (cero o más)
15. Cuantificador + (uno o más)
16. Cuantificador ? (cero o uno)
17. Cuantificador {n} (exactamente n)
18. Cuantificador {n,} (n o más)
19. Cuantificador {n,m} (entre n y m)
20. Cuantificadores perezosos (lazy): *? +? ?? {n,m}?
21. Clases de caracteres: [abc]
22. Rangos: [a-z], [0-9]
23. Negación: [^abc]
24. Clases predefinidas: \d (dígito)
25. \D (no dígito)
26. \w (word character)
27. \W (no word character)
28. \s (whitespace)
29. \S (no whitespace)
30. \b (word boundary)
31. En Java regex, doble backslash: \\d, \\w, \\s
32. Anclajes: ^ (inicio de línea)
33. $ (fin de línea)
34. Alternancia: a|b
35. Grupos: (expresión)
36. Grupos con nombre: (?<nombre>expresión)
37. Grupos sin captura: (?:expresión)
38. Backreferences: \1, \2 (\\1, \\2 en Java)
39. Named backreferences: \k<nombre>
40. Lookahead positivo: (?=expresión)
41. Lookahead negativo: (?!expresión)
42. Lookbehind positivo: (?<=expresión)
43. Lookbehind negativo: (?<!expresión)
44. Matcher.group(n) para grupos por número
45. Matcher.group("nombre") para grupos con nombre
46. Matcher.groupCount() para contar grupos
47. Matcher.replaceAll() para reemplazar todas
48. Matcher.replaceFirst() para reemplazar la primera
49. Matcher.appendReplacement() y appendTail()
50. Pattern.compile con flags
51. Pattern.CASE_INSENSITIVE
52. Pattern.MULTILINE
53. Pattern.DOTALL
54. Pattern.COMMENTS (Pattern.COMMENTS)
55. Pattern.UNICODE_CHARACTER_CLASS
56. Pattern.LITERAL para tratar regex como literal
57. Inline flags: (?i), (?m), (?s)
58. Pattern.split() para dividir por patrón
59. String.split(regex) usa Pattern internamente
60. Compilar una vez, usar muchas: reutilizar Pattern
61. Rendimiento: Pattern.compile vs String.matches
62. Pattern es thread-safe, Matcher no
63. Validación de email con regex
64. Validación de URL con regex
65. Validación de teléfono con regex
66. Validación de IP con regex
67. Extraer datos de un log
68. Parsear CSV con regex
69. Reemplazar múltiples espacios con uno
70. Reemplazar HTML tags
71. Formatear texto con regex
72. Matcher como iterador: while (matcher.find())
73. Capturar grupos en un loop
74. Regex y cultura (Locale)
75. ReDoS (Regular Expression Denial of Service)
76. Protegerse de ReDoS con patrones seguros
77. Timeout en regex (no nativo, manual)
78. java.util.regex vs org.apache.commons.lang3.Regex
79. Alternativas a regex: String.contains(), startsWith()
80. Cuándo usar regex vs métodos de String
81. Regex en validación de formularios
82. Regex en routing patterns
83. Regex en log parsing
84. Regex en search & replace masivo
85. Regex con Files.lines() para procesar archivos
86. Regex con streams para filtrar líneas
87. Pattern.asPredicate() para usar en streams
88. Pattern.asMatchPredicate() (Java 11)
89. Scanner con regex para tokenizar
90. Named groups y su importancia para legibilidad
91. Regex en Spring @RequestMapping patterns
92. Regex en URL matching
93. Regex y Unicode: \p{L}, \p{N}
94. Unicode properties en Java regex
95. Character classes en Java regex
96. POSIX classes en Java regex (limitadas)
97. Atomic groups y possessive quantifiers
98. Backtracking y performance
99. Regex debugger en IntelliJ
100. Resumen: patrones regex comunes como referencia

---

## MÓDULO 26: RECORDS, SEALED CLASSES Y PATTERN MATCHING

**Descripción:** Este módulo agrupa las características modernas de Java que transforman la forma de escribir código. Los records proporcionan clases de datos concisas. Las sealed classes controlan la herencia. El pattern matching permite evaluaciones complejas y declarativas. Son features de Java 16-21 que todo desarrollador moderno debe dominar.

1. Records (Java 16): clases inmutables para datos
2. record Persona(String nombre, int edad)
3. Records son final por defecto
4. Records: constructor canónico generado automáticamente
5. Records: equals(), hashCode(), toString() automáticos
6. Records: getters (métodos con nombre del campo)
7. Records NO tienen setters (son inmutables)
8. Compact canonical constructor para validación
9. Custom constructor adicional
10. Records con métodos personalizados
11. Records con métodos estáticos
12. Records implementan interfaces
13. Records como inner classes
14. Records genéricos: record Pair<A, B>(A first, B second)
15. Local records (dentro de métodos)
16. Records y pattern matching
17. Records y desestructuración (record patterns, Java 21)
18. Records como Value Objects en DDD
19. Records como DTOs
20. Records como keys en Map (hashCode/equals automáticos)
21. Records en colecciones
22. Records y JSON (Jackson, Gson)
23. Records y JPA (limitaciones)
24. Records y serialización
25. Records y Lombok @Value: comparativa
26. Records vs clases regulares: cuándo usar cada uno
27. Records vs enums para datos simples
28. Sealed Classes (Java 17): controlar la herencia
29. sealed class Shape permits Circle, Rectangle, Triangle
30. sealed interface permits ...
31. Las clases permitidas deben ser: final, sealed, o non-sealed
32. final subclass: no permite más herencia
33. sealed subclass: permite más herencia controlada
34. non-sealed subclass: abre la jerarquía
35. Sealed classes y pattern matching exhaustivo
36. El compilador verifica exhaustividad en switch
37. Sealed classes con records
38. Sealed hierarchies como discriminated unions
39. Sealed interfaces
40. Sealed y la relación con pattern matching
41. Pattern matching (evolución en Java 14-21)
42. Pattern matching for instanceof (Java 16)
43. if (obj instanceof String s) { ... }
44. El scope de la variable de patrón
45. Pattern matching con clases base
46. Pattern matching con interfaces
47. Guarded patterns con && (Java 21)
48. Pattern matching en switch (Java 21)
49. switch (obj) { case Integer i -> ...; case String s -> ... }
50. Null handling en switch: case null -> ...
51. Guarded patterns en switch: case String s when s.length() > 5
52. Exhaustividad con sealed types en switch
53. Record patterns (Java 21)
54. Desestructurar records: case Point(int x, int y) -> ...
55. Nested record patterns
56. Record patterns en for-each
57. Record patterns con guarded patterns
58. Array patterns (no disponible aún en Java)
59. Pattern matching y Optional
60. Pattern matching y builders
61. Pattern matching como alternativa a Visitor pattern
62. Pattern matching como alternativa a instanceof chains
63. Pattern matching y polimorfismo
64. Cuándo usar pattern matching vs polimorfismo
65. Pattern matching en expresiones switch
66. Switch expressions con ->
67. Switch expressions con yield
68. Switch expressions como expresiones (asignables)
69. Switch expressions exhaustivas
70. Diferencia switch statement y switch expression
71. Arrow form vs colon form en switch
72. Ejemplo: calculadora con switch expression
73. Ejemplo: validación con pattern matching
74. Ejemplo: procesamiento de AST con records y sealed
75. Ejemplo: Expression tree con sealed y records
76. Records, sealed y pattern matching juntos
77. Modelar dominio con estos tres features
78. Migrar código legacy a records
79. Migrar instanceof chains a pattern matching
80. Migrar class hierarchies a sealed
81. Records y serialization frameworks
82. Records y JSON serialization
83. Sealed classes y JPA
84. Sealed classes y frameworks que necesitan herencia
85. Records y testing
86. Pattern matching y testing
87. Records y Lombok: ¿cuándo usar cada uno?
88. Records y Immutables framework
89. Records y AutoValue de Google
90. Records y null safety
91. Records con Optional fields
92. Records y collections mutables (shallow immutability)
93. Records con defensive copy de collections
94. Records y Stream API
95. Pattern matching en streams
96. Records y functional programming
97. Records y builder pattern
98. Sealed classes y versioning
99. Records y pattern matching en Java 22+
100. Resumen: cuándo usar records, sealed y pattern matching

---

## MÓDULO 27: CONCURRENCIA AVANZADA Y VIRTUAL THREADS

**Descripción:** Java 21 introduce Virtual Threads, revolucionando la concurrencia. Aprenderás structured concurrency, scoped values, reactive programming con CompletableFuture, y los patrones avanzados de concurrencia que se usan en producción.

1. Revisión de ExecutorService y thread pools
2. Virtual Threads en profundidad (Java 21)
3. Thread.ofVirtual().name("vt-", 0).start(runnable)
4. Thread.ofVirtual().factory() para crear factory
5. Executors.newVirtualThreadPerTaskExecutor()
6. Virtual threads son muy baratos de crear
7. Crear millones de virtual threads
8. Virtual threads usan carrier threads (ForkJoinPool)
9. Pinned: virtual thread que bloquea carrier thread
10. Causas de pinning: synchronized blocks, native methods
11. Detectar pinning con -Djdk.tracePinnedThreads=full
12. Usar ReentrantLock en lugar de synchronized
13. Virtual threads y I/O: non-blocking automáticamente
14. Virtual threads y blocking I/O: suspenden solo el virtual thread
15. Virtual threads y ThreadLocal: precaución
16. Virtual threads y Semaphore para limitar
17. Structured Concurrency (Preview, Java 21)
18. StructuredTaskScope.ShutdownOnFailure
19. StructuredTaskScope.ShutdownOnSuccess
20. try (var scope = new StructuredTaskScope.ShutdownOnFailure()) { }
21. scope.fork(() -> tarea1)
22. scope.fork(() -> tarea2)
23. scope.join().throwIfFailed()
24. Structured vs unstructured concurrency
25. Scoped Values (Preview, Java 21)
26. ScopedValue.newInstance()
27. ScopedValue.where(key, value).run(() -> { ... })
28. Scoped Values vs ThreadLocal
29. Scoped Values son inmutables y se propagan correctamente
30. Scoped Values y virtual threads
31. CompletableFuture revisión profunda
32. CompletableFuture.allOf() con gran número de futures
33. CompletableFuture con virtual threads
34. CompletableFuture.supplyAsync(supplier, virtualExecutor)
35. Composing futures con thenCompose y thenCombine
36. CompletableFuture con timeout
37. orTimeout() y completeOnTimeout() (Java 9)
38. CompletableFuture y exception handling
39. exceptionally(), handle(), whenComplete()
40. CompletableFuture y Circuit Breaker
41. Reactive Streams: Flow API (Java 9)
42. Flow.Publisher<T>
43. Flow.Subscriber<T>
44. Flow.Subscription
45. Flow.Processor<T, R>
46. SubmissionPublisher
47. Reactive Streams specification
48. Backpressure en reactive streams
49. Project Reactor: Flux y Mono
50. Flux<T>: stream de 0-N elementos
51. Mono<T>: stream de 0-1 elementos
52. Flux.fromIterable() y Flux.just()
53. Flux.map(), filter(), flatMap()
54. Flux.subscribe()
55. Mono.fromCallable() y Mono.just()
56. Mono.flatMap() y Mono.zip()
57. Reactor y schedulers: Schedulers.boundedElastic()
58. Reactor y virtual threads
59. RxJava como alternativa (ReactiveX)
60. Observable, Single, Completable
61. RxJava operators
62. RxJava vs Reactor: comparativa
63. Concurrency patterns: Producer-Consumer
64. Concurrency patterns: Reader-Writer
65. Concurrency patterns: Fan-out/Fan-in
66. Concurrency patterns: Pipeline
67. Concurrency patterns: Map-Reduce
68. Concurrency patterns: Work distribution
69. Thread-safe patterns: Immutable objects
70. Thread-safe patterns: Copy-on-write
71. Thread-safe patterns: Message passing
72. Thread-safe patterns: Actor model (concepto)
73. Akka para Java (introducción)
74. Virtual threads y Spring Boot 3.2+
75. Spring Boot y virtual threads: spring.threads.virtual.enabled=true
76. Tomcat con virtual threads
77. JDBC con virtual threads
78. Hibernate con virtual threads
79. HTTP clients con virtual threads
80. Virtual threads en microsservices
81. Performance: virtual threads vs platform threads
82. Benchmarking con JMH
83. JMH: @Benchmark, @State, @Param
84. JMH: @Warmup, @Measurement, @Fork
85. JMH con virtual threads
86. Diagnosing concurrent issues: jstack
87. Java Flight Recorder: thread events
88. Thread dumps y análisis
89. Deadlock detection con jconsole
90. ThreadMXBean para monitoreo
91. Testing concurrent code con jcstress
92. Thread safety annotations: @GuardedBy, @ThreadSafe
93. Error-prone de Google para concurrency bugs
94. SpotBugs para concurrency analysis
95. ConcurrentHashMap internals: segment locking
96. LongAdder vs AtomicLong: high contention
97. StampedLock vs ReentrantReadWriteLock
98. Semaphore y virtual threads
99. Rate limiting con Semaphore
100. Resumen: guía de concurrencia moderna en Java

---

## MÓDULO 28: REFLEXIÓN Y ANOTACIONES

**Descripción:** La reflexión permite inspeccionar y manipular tipos en runtime, y las anotaciones proporcionan metadatos. Aprenderás java.lang.reflect, crear anotaciones personalizadas, y entender cuándo la reflexión es apropiada y cuándo debe eviterse.

1. ¿Qué es la reflexión (reflection)?
2. java.lang.reflect package
3. Obtener Class con .getClass()
4. Obtener Class con ClassName.class
5. Class.forName("com.example.MyClass")
6. Class<T> como la clase central de reflexión
7. Class: getName(), getSimpleName(), getCanonicalName()
8. Class: isInterface(), isEnum(), isRecord(), isSealed()
9. Class: isAnnotation(), isAnonymousClass()
10. Class: isPrimitive(), isArray()
11. Class: getSuperclass()
12. Class: getInterfaces()
13. Class: getPackage()
14. Class: getModifiers() y Modifier class
15. Obtener constructores: getConstructors()
16. Obtener constructores declarados: getDeclaredConstructors()
17. Constructor.newInstance(args) para crear instancias
18. Obtener métodos: getMethods() (públicos e heredados)
19. Obtener métodos declarados: getDeclaredMethods()
20. Method.invoke(obj, args) para invocar
21. Method: getName(), getReturnType(), getParameterTypes()
22. Obtener campos: getFields() (públicos)
23. Obtener campos declarados: getDeclaredFields()
24. Field.get(obj) y Field.set(obj, value)
25. Field: getName(), getType(), getModifiers()
26. setAccessible(true) para acceder a private
27. Obtener interfaces: getInterfaces()
28. Obtener annotations: getAnnotations()
29. getDeclaredAnnotations()
30. getAnnotation(Class<A>)
31. isAnnotationPresent(Class<A>)
32. Modifiers: Modifier.isPublic(), isStatic(), isFinal()
33. Modifier.toString(modifiers)
34. Diferencia entre get y getDeclared
35. get incluye miembros heredados (solo públicos)
36. getDeclared solo miembros de la clase (cualquier visibilidad)
37. Anotaciones: metadatos decorativos
38. Declarar una anotación: @interface
39. @Target para restringir dónde se aplica
40. ElementType: TYPE, METHOD, FIELD, PARAMETER
41. ElementType: CONSTRUCTOR, LOCAL_VARIABLE, PACKAGE
42. @Retention para controlar persistencia
43. RetentionPolicy: SOURCE, CLASS, RUNTIME
44. @Documented para incluir en Javadoc
45. @Inherited para heredar en subclases
46. @Repeatable para anotaciones repetibles
47. Elementos de anotación: String value() default ""
48. Tipos permitidos en elementos: primitivos, String, Class, enums, anotaciones, arrays
49. Anotaciones built-in: @Override
50. @Deprecated y @Deprecated(since, forRemoval)
51. @SuppressWarnings("unchecked")
52. @FunctionalInterface
53. @SafeVarargs
54. @Native
55. Anotaciones de Spring: @Component, @Service, @Repository
56. @Autowired, @Qualifier, @Value
57. @Configuration, @Bean
58. @RequestMapping, @GetMapping, @PostMapping
59. @RequestParam, @PathVariable, @RequestBody
60. Jakarta Validation: @NotNull, @Size, @Min, @Max
61. @Valid para activar validación
62. Custom validation annotations
63. @Constraint(validatedBy = ...)
64. Anotaciones de JPA: @Entity, @Table, @Id
65. @Column, @OneToMany, @ManyToOne
66. Anotaciones de testing: @Test, @BeforeEach, @AfterEach
67. @DisplayName, @Tag, @ParameterizedTest
68. @ExtendWith, @MockitoExtension
69. @Mock, @InjectMocks, @Spy
70. Procesamiento de anotaciones en compile-time
71. Annotation processing API
72. AbstractProcessor para crear procesadores
73. Process annotations con RoundEnvironment
74. Generate code con annotation processing
75. Lombok como annotation processor
76. MapStruct como annotation processor
77. Dagger para DI compile-time
78. Performance de reflexión: es lenta
79. Caching de resultados de reflexión
80. MethodHandle como alternativa más rápida
81. MethodHandles.Lookup
82. MethodHandle.invoke() y invokeExact()
83. VarHandle (Java 9) para acceso a variables
84. VarHandle: alternativa a volatile + AtomicX
85. MethodHandles vs reflection: performance
86. Dynamic proxies con java.lang.reflect.Proxy
87. InvocationHandler interface
88. Proxy.newProxyInstance()
89. Dynamic proxies en Spring AOP
90. CGLIB proxies en Spring
91. Reflection en frameworks: Spring, Hibernate
92. Reflection en testing: Mockito usa reflection
93. Reflection en serialization: Jackson, Gson
94. Reflection en DI containers
95. Alternativas sin reflexión: compile-time DI, source gen
96. GraalVM Native Image y reflection limits
97. ReflectConfig.json para GraalVM
98. @RegisterForReflection de Quarkus
99. Cuándo usar reflexión: frameworks, plugins
100. Resumen: reflexión como último recurso

---

## MÓDULO 29: JAVA MODULE SYSTEM (JPMS)

**Descripción:** El Java Platform Module System (Java 9) permite modularizar aplicaciones grandes. Aprenderás a crear módulos, definir exports y requires, entender el modulepath vs classpath, y los desafíos de modularizar código existente.

1. ¿Qué es el Java Platform Module System (JPMS)?
2. El problema: classpath hell
3. module-info.java: el descriptor de módulo
4. requires: declarar dependencias de módulos
5. exports: exponer packages públicos
6. open: abrir packages para reflexión
7. exports...to: exportar a módulos específicos
8. provides...with: servicio con implementación
9. uses: consumir un servicio
10. Module types: application, library, automatic, unnamed
11. Módulo unnamed: todo en el classpath
12. Módulo automatic: JAR sin module-info
13. Crear un módulo: carpeta con module-info.java
14. Compilar módulos: javac -d out --module-source-path src -m module.name
15. Ejecutar módulos: java --module-path out -m module.name/module.main.Class
16. Modular JAR files
17. jlink para crear imágenes de runtime personalizadas
18. jlink --module-path $JAVA_HOME/jmods:mods --add-modules com.app --output dist
19. jlink y reducción de tamaño de distribución
20. jmod para crear módulos nativos
21. jdeps para análisis de dependencias
22. jdeps --module-path mods --check com.app
23. Migrar de classpath a modulepath
24. El unnamed module como puente
25. Automatic modules: JAR como módulo automático
26. Module path vs classpath
27. Strong encapsulation: no acceso a internal APIs
28. --add-opens para abrir módulos del JDK
29. --add-exports para exportar módulos del JDK
30. --add-reads para agregar lecturas
31. java.base: el módulo raíz
32. Módulos del JDK: java.sql, java.http, java.logging
33. Servicios con provides/uses
34. ServiceLoader.load(Module.class)
35. Plugin architecture con JPMS
36. Modular monolith architecture
37. Módulos y testing
38. --add-modules para tests
39. JUnit 5 y modules
40. Maven y modules: multi-module project
41. Gradle y modules
42. Spring Boot y modules
43. JPMS y reflection: requires open
44. JPMS y Spring: los desafíos
45. --add-opens para frameworks que usan reflection
46. JPMS en producción: ¿se usa mucho?
47. Microservices: JPMS menos relevante
48. Monolitos modulares: JPMS más relevante
49. GraalVM y JPMS
50. jlink para Docker images optimizadas

---

## MÓDULO 30: JVM INTERNALS, JIT Y GARBAGE COLLECTOR

**Descripción:** Entender la JVM es lo que distingue a un desarrollador senior. Aprenderás cómo funciona el JIT, los diferentes GC (G1, ZGC, Shenandoah), la gestión de memoria, y cómo diagnosticar problemas de rendimiento.

1. ¿Qué es la JVM y cómo funciona?
2. Class loading y ClassLoader
3. Bootstrap ClassLoader, Platform ClassLoader, Application ClassLoader
4. Custom ClassLoaders
5. Class loading delegation model
6. Linking: verify, prepare, resolve
7. Initialization: static blocks y static fields
8. Memory areas: heap, stack, method area, PC register
9. Heap: donde viven los objetos
10. Stack: frames por cada método invocado
11. Method Area / Metaspace: información de clases
12. Metaspace reemplazó PermGen (Java 8)
13. -XX:MaxMetaspaceSize para limitar Metaspace
14. JIT compilation: HotSpot JIT
15. Client compiler (C1) vs Server compiler (C2)
16. Tiered compilation: C1 → C2
17. Deoptimization: cuando el JIT se equivoca
18. Inlining de métodos
19. Escape analysis: determinar si objetos escapan del thread
20. Scalar replacement: reemplazar objetos por sus campos
21. Loop optimizations
22. Intrinsics: operaciones optimizadas por hardware
23. Garbage Collection: ¿por qué existe?
24. Reachability analysis
25. Generational GC: Young, Old (Tenured)
26. Young Generation: Eden, Survivor spaces
27. Minor GC: collection del Young Generation
28. Major GC / Full GC: collection del Old Generation
29. Mark-Compact algorithm
30. Mark-Sweep algorithm
31. Copying algorithm
32. G1 Garbage Collector (default desde Java 9)
33. G1: region-based, incremental
34. G1: pause time goals con -XX:MaxGCPauseMillis
35. ZGC: ultra-low latency (Java 11+)
36. ZGC: pausas < 1ms
37. ZGC: -XX:+UseZGC
38. ZGC generational (Java 21)
39. Shenandoah GC
40. Shenandoah: concurrent compaction
41. -XX:+UseShenandoahGC
42. Serial GC: -XX:+UseSerialGC
43. Parallel GC: -XX:+UseParallelGC
44. Epsilon GC: no-op GC (benchmarking)
45. -XX:+UseEpsilonGC
46. GC logging: -Xlog:gc*
47. -Xlog:gc*:file=gc.log:time,uptime,level,tags
48. GC tuning: -Xms y -Xmx
49. -Xmn para young generation size
50. -XX:NewRatio y -XX:SurvivorRatio
51. Java Mission Control (JMC)
52. Java Flight Recorder (JFR)
53. jcmd para comandos JVM
54. jmap para heap dumps
55. jstack para thread dumps
56. jstat para estadísticas GC
57. jinfo para configuración JVM
58. VisualVM para profiling
59. Heap dumps: análisis con MAT (Memory Analyzer Tool)
60. OutOfMemoryError: causas comunes
61. -XX:+HeapDumpOnOutOfMemoryError
62. Memory leaks en Java
63. Detectar memory leaks: heap dump analysis
64. GC roots: threads, static fields, JNI
65. Strong references, Soft references, Weak references
66. Phantom references
67. WeakHashMap y su relación con GC
68. ReferenceQueue para notificaciones de GC
69. -XX:SoftRefLRUPolicyMSPerMB
70. Object allocation: TLAB (Thread Local Allocation Buffer)
71. -XX:+UseTLAB
72. Large object allocation y humongous regions (G1)
73. GC pause times y SLAs
74. Latency vs throughput: elegir GC
75. G1 vs ZGC vs Shenandoah: comparativa
76. GC en containers Docker
77. -XX:MaxRAMPercentage para containers
78. -XX:ActiveProcessorCount para containers
79. GC y virtual threads
80. GraalVM Native Image y GC
81. Native Image: SubstrateVM GC
82. AOT compilation y su impacto en GC
83. JIT warmup y su impacto
84. Tiered compilation levels
85. -XX:-TieredCompilation para solo C2
86. JVM ergonomics: auto-tuning
87. Performance testing con JMH
88. JMH: microbenchmarks precisos
89. -prof gc en JMH para medir allocations
90. -prof perfnorm en JMH
91. Benchmarking GC: allocation rates
92. String deduplication: -XX:+UseStringDeduplication
93. Compact strings en Java 9+
94. JVMCI (JVM Compiler Interface) y Graal compiler
95. JEPs relevantes para GC y JVM
96. Java 21: generational ZGC
97. Java 21: compact object headers
98. Virtual threads y GC impact
99. JVM tuning para diferentes workloads
100. Resumen: reglas de oro para gestión de memoria en Java

---

## MÓDULO 31: MAVEN Y GRADLE

**Descripción:** Maven y Gradle son los dos sistemas de build más usados en Java. Aprenderás a usar ambos, crear proyectos, gestionar dependencias, configurar plugins, y entender cuándo usar cada uno.

1. ¿Qué es un sistema de build?
2. Maven: filosofía "convention over configuration"
3. La estructura de carpetas estándar de Maven
4. src/main/java, src/main/resources
5. src/test/java, src/test/resources
6. El archivo pom.xml: Project Object Model
7. groupId, artifactId, version (GAV coordinates)
8. packaging: jar, war, pom
9. Dependencies en pom.xml
10. <dependency> con groupId, artifactId, version
11. Dependency scope: compile, test, provided, runtime
12. Dependency management: <dependencyManagement>
13. BOM (Bill of Materials)
14. Import scope: import de BOM
15. Transitive dependencies
16. Dependency conflicts y resolución
17. Exclusion de dependencias transitivas
18. Maven repositories: Central, local, private
19. <repositories> en pom.xml
20. Settings.xml: configuración global
21. Profiles en Maven
22. Plugins de Maven: compiler, surefire, jar, deploy
23. <build> <plugins> en pom.xml
24. maven-compiler-plugin para configurar Java version
25. maven-surefire-plugin para ejecutar tests
26. maven-failsafe-plugin para integration tests
27. maven-jar-plugin para crear JAR
28. maven-war-plugin para crear WAR
29. maven-shade-plugin para uber-jar
30. maven-assembly-plugin para distribuciones
31. maven-source-plugin para source JAR
32. maven-javadoc-plugin para javadoc JAR
33. maven-release-plugin para releases
34. mvn clean install: el comando más usado
35. mvn clean package
36. mvn test
37. mvn compile
38. mvn dependency:tree
39. mvn dependency:analyze
40. Maven lifecycle: validate, compile, test, package, verify, install, deploy
41. Phases y goals
42. Multi-module projects con Maven
43. <modules> en pom.xml padre
44. Parent POM y child POM
45. Inheritance en POM
46. Effective POM: mvn help:effective-pom
47. Gradle: build system basado en Groovy/Kotlin DSL
48. build.gradle (Groovy DSL) o build.gradle.kts (Kotlin DSL)
49. Gradle: plugins, dependencies, tasks
50. apply plugin: 'java'
51. plugins { id 'java' }
52. repositories { mavenCentral() }
53. dependencies { implementation '...' }
54. Dependency configurations: implementation, api, compileOnly
55. testImplementation, runtimeOnly
56. Gradle Wrapper: gradlew
57. ./gradlew build, ./gradlew test
58. Gradle tasks: build, test, clean, jar
59. Custom tasks en Gradle
60. Gradle incremental builds
61. Gradle build cache
62. Gradle configuration cache
63. Multi-module projects con Gradle
64. settings.gradle para incluir subproyectos
65. Dependencies entre subproyectos
66. Gradle vs Maven: tabla comparativa
67. Cuándo usar Maven
68. Cuándo usar Gradle
69. Spring Boot Maven Plugin
70. Spring Boot Gradle Plugin
71. spring-boot-maven-plugin: repackage
72. Crear executable JAR con Spring Boot plugin
73. Dockerfile con Maven/Gradle
74. Jib plugin para Docker sin Dockerfile
75. Maven Wrapper: mvnw
76. Version properties en pom.xml
77. <properties> para versiones centralizadas
78. Dependency version ranges (no recomendado)
79. SNAPSHOTS: versiones de desarrollo
80. Release versions: versiones estables
81. Semantic versioning
82. maven-enforcer-plugin para reglas
83. RequireJavaVersion, RequireMavenVersion
84. BanDuplicateClasses
85. Dependency convergence
86. OWASP dependency check plugin
87. SpotBugs plugin para análisis de bugs
88. Checkstyle plugin para estilo de código
89. PMD plugin para análisis estático
90. JaCoCo plugin para cobertura de código
91. Cobertura de código en CI/CD
92. Publish a Maven Central
93. Sonatype OSSRH como repositorio
94. GPG signing de artifacts
95. Gradle publishing a Maven Central
96. Gradle version catalogs (libs.versions.toml)
97. Renovate/Dependabot para actualizaciones
98. Gradle Build Scans
99. Maven y Kotlin DSL
100. Resumen: guía de selección Maven vs Gradle

---

## MÓDULO 32: INYECCIÓN DE DEPENDENCIAS Y SPRING CORE

**Descripción:** La Inyección de Dependencias es fundamental en el desarrollo Java moderno. Aprenderás el concepto de IoC, el contenedor DI de Spring Framework, los ciclos de vida (Singleton, Prototype, Request, Session), y cómo usar DI en aplicaciones Java.

1. ¿Qué es la Inyección de Dependencias?
2. El problema del acoplamiento directo (new)
3. Inversión de Control (IoC)
4. Dependency Inversion Principle (DIP)
5. Constructor injection (recomendado)
6. Setter injection
7. Field injection con @Autowired (no recomendado)
8. ApplicationContext: el contenedor de Spring
9. BeanFactory: la interfaz base del contenedor
10. @Component para registrar beans
11. @Service para servicios
12. @Repository para acceso a datos
13. @Controller y @RestController para web
14. @Configuration para clases de configuración
15. @Bean para definir beans en configuración
16. @ComponentScan para escanear packages
17. @Autowired para inyección automática
18. @Qualifier para desambiguar
19. @Primary para bean preferido
20. @Value para inyectar valores de configuración
21. @PropertySource para cargar properties
22. Scope: @Scope("singleton") - default
23. Scope: @Scope("prototype") - nueva instancia
24. Scope: @Scope("request") - por HTTP request
25. Scope: @Scope("session") - por HTTP session
26. Scope: @Scope("application") - por ServletContext
27. Singleton scope: una instancia por contenedor
28. Prototype scope: nueva instancia cada vez
29. @Lazy para carga perezosa
30. @PostConstruct para inicialización post-DI
31. @PreDestroy para cleanup
32. InitializingBean y DisposableBean (interfaces)
33. @Bean(initMethod, destroyMethod)
34. Bean lifecycle en Spring
35. Bean post-processors: BeanPostProcessor
36. ApplicationContextAware para obtener el contexto
37. Factory methods en @Configuration classes
38. @Import para importar configuraciones
39. @ImportResource para XML configuration
40. Profiles con @Profile("dev"), @Profile("prod")
41. spring.profiles.active en application.properties
42. @ConditionalOnProperty
43. @ConditionalOnClass
44. @ConditionalOnMissingBean
45. Conditional annotations en Spring Boot
46. Property injection con @Value("${key}")
47. Default values: @Value("${key:defaultValue}")
48. SpEL (Spring Expression Language): @Value("#{...}")
49. Environment para acceso programático a properties
50. @ConfigurationProperties para strong-typed config
51. @ConfigurationProperties(prefix = "app.database")
52. @Validated con Data Annotations
53. ApplicationContext.getBeansOfType()
54. ApplicationContext.getBean()
55. GenericApplicationContext para registro programático
56. BeanDefinition para definiciones de beans
57. FactoryBean<T> para beans complejos
58. Proxy beans con @Scope(proxyMode)
59. Scoped proxies para inyectar scopes cortos en largos
60. @Lookup para métodos de lookup
61. Event handling con ApplicationEvent
62. @EventListener para escuchar eventos
63. ApplicationEventPublisher para publicar
64. @Transactional para transacciones (introducción)
65. Transaction management en Spring
66. AOP (Aspect-Oriented Programming) en Spring
67. @Aspect, @Before, @After, @Around
68. Pointcut expressions: execution(* com.example..*.*(..))
69. @Pointcut para reutilizar pointcuts
70. JoinPoint para acceder al contexto del método
71. ProceedingJoinPoint para @Around
72. AOP proxies en Spring
73. CGLIB proxies vs JDK proxies
74. Spring Testing con @SpringJUnitConfig
75. @MockBean en Spring Boot tests
76. ApplicationContext en tests
77. @DirtiesContext para resetear contexto
78. Spring y virtual threads (Spring Boot 3.2+)
79. Spring y records
80. Spring y sealed classes
81. GraalVM Native Image y Spring
82. Spring AOT processing
83. spring-boot-starter-actuator para monitoreo
84. Health checks con Actuator
85. Metrics con Actuator
86. Info endpoint
87. Custom health indicators
88. @Endpoint para custom actuator endpoints
89. Spring Boot DevTools para desarrollo
90. LiveReload y automatic restart
91. Remote debugging
92. Testing con @SpringBootTest
93. Testing con @WebMvcTest
94. Testing con @DataJpaTest
95. Testing con @TestConfiguration
96. @SpyBean y @MockBean
97. TestRestTemplate y WebTestClient
98. WireMock para APIs externas
99. Testcontainers para base de datos
100. Resumen: reglas de oro para DI y Spring Core

---

## MÓDULO 33: LOGGING Y MONITOREO

**Descripción:** Sin logging y monitoreo, una aplicación en producción es una caja negra. Aprenderás SLF4J, Logback, Log4j2, structured logging, métricas con Micrometer, distributed tracing, y health checks.

1. ¿Por qué el logging es esencial?
2. System.out.println no es logging profesional
3. SLF4J: Simple Logging Facade for Java
4. SLF4J como fachada (facade pattern)
5. LoggerFactory.getLogger(ClassName.class)
6. logger.trace(), debug(), info(), warn(), error()
7. Log levels: TRACE, DEBUG, INFO, WARN, ERROR
8. Parameterized logging: logger.info("User {} logged in", userId)
9. Evitar concatenación: no logger.info("User " + id)
10. Logger con excepciones: logger.error("Error", exception)
11. isDebugEnabled() para código costoso
12. MDC (Mapped Diagnostic Context) para request tracking
13. MDC.put("requestId", uuid)
14. %X{requestId} en el pattern de log
15. Logback: el implementador por defecto de Spring Boot
16. logback.xml para configuración
17. logback-spring.xml para configuración con Spring
18. <appender>: ConsoleAppender, FileAppender, RollingFileAppender
19. <encoder> y <pattern>
20. <root level="INFO">
21. <logger name="com.example" level="DEBUG">
22. Rolling policy: TimeBasedRollingPolicy
23. SizeAndTimeBasedRollingPolicy
24. maxHistory para retención
25. totalSizeCap para límite total
26. AsyncAppender para logging asíncrono
27. Log4j2: alternativa popular
28. log4j2.xml para configuración
29. Log4j2 appenders: Console, File, RollingFile
30. Log4j2: AsyncLogger y AsyncAppender
31. Log4j2: LMAX Disruptor para async
32. java.util.logging (JUL): el logging nativo
33. JUL: Logger, Handler, Formatter
34. JUL: por qué no usarlo directamente
35. Structured logging: JSON format
36. Logback JSON encoder con logstash-logback-encoder
37. {"timestamp":"...", "level":"INFO", "message":"...", "userId":"..."}
38. Structured logging y ELK Stack
39. Elasticsearch, Logstash, Kibana
40. Logstash para procesar logs
41. Kibana para visualizar logs
42. Grafana + Loki como alternativa
43. Correlation IDs para request tracking
44. Distributed logging en microservices
45. SLF4J MDC y correlation IDs
46. Spring Cloud Sleuth (ahora Micrometer Tracing)
47. Micrometer: facade para métricas
48. MeterRegistry para registrar métricas
49. Counter para contar eventos
50. Timer para medir duraciones
51. Gauge para valores actuales
52. DistributionSummary para distribuciones
53. @Timed annotation en Spring
54. @Counted annotation
55. Metrics con tags/dimensions
56. MeterFilters para transformar métricas
57. Exportar métricas a Prometheus
58. Prometheus: almacenamiento de métricas
59. Grafana para dashboards
60. micrometer-registry-prometheus
61. management.endpoints.web.exposure.include=prometheus
62. OpenTelemetry para .NET/Java
63. OpenTelemetry Java agent
64. opentelemetry-javaagent.jar para auto-instrumentación
65. Distributed tracing con OpenTelemetry
66. Trace y Span concepts
67. W3C Trace Context propagation
68. Exportar traces a Jaeger
69. Exportar traces a Zipkin
70. Micrometer Tracing (reemplazo de Sleuth)
71. Brave como tracer implementation
72. Health checks en Spring Boot Actuator
73. /actuator/health endpoint
74. Health indicators: DiskSpace, DataSource, Custom
75. Liveness y Readiness en Kubernetes
76. /actuator/health/liveness
77. /actuator/health/readiness
78. Custom health indicators con AbstractHealthIndicator
79. Health groups para Kubernetes probes
80. Logging y GDPR: no logear PII
81. Log retention policies
82. Log rotation strategies
83. Centralized logging architectures
84. Alerting basado en logs
85. Alerting basado en métricas
86. Dashboards de observabilidad
87. The Three Pillars: Logs, Metrics, Traces
88. RED method: Rate, Errors, Duration
89. USE method: Utilization, Saturation, Errors
90. SLIs, SLOs, SLAs
91. Structured logging en tests
92. Verificar logs en tests
93. Logging performance: evitar allocations
94. High-performance logging con Log4j2
95. LoggerMessage en Spring (optimización)
96. Logging en background services
97. Logging en middleware/filters
98. Request logging con Logbook (Zalando)
99. Observability-driven development
100. Resumen: stack de observabilidad recomendado

---

## MÓDULO 34: JDBC Y SQL CON JAVA

**Descripción:** Antes de usar ORMs, necesitas entender JDBC y SQL. Aprenderás a conectarte a bases de datos, ejecutar consultas, usar parámetros, leer datos con ResultSet, trabajar con transacciones, y escribir SQL eficiente.

1. ¿Qué es JDBC?
2. java.sql package
3. JDBC drivers: Type 1, 2, 3, 4
4. Driver manager: DriverManager.getConnection()
5. Connection strings / JDBC URLs
6. PostgreSQL: jdbc:postgresql://host:port/database
7. MySQL: jdbc:mysql://host:port/database
8. H2: jdbc:h2:mem:testdb (in-memory)
9. SQLite: jdbc:sqlite:database.db
10. Abrir y cerrar conexiones: Connection.close()
11. try-with-resources para gestión automática
12. Connection pooling: HikariCP
13. HikariConfig y HikariDataSource
14. Maximum pool size, minimum idle
15. Connection timeout, idle timeout
16. Statement para consultas simples
17. executeQuery() para SELECT
18. executeUpdate() para INSERT, UPDATE, DELETE
19. execute() para cualquier SQL
20. PreparedStatement para consultas parametrizadas
21. PreparedStatement evita SQL injection
22. setString(), setInt(), setDouble(), setDate()
23. setTimestamp() para fechas con hora
24. setNull() para valores null
25. CallableStatement para stored procedures
26. registerOutParameter() para parámetros de salida
27. ResultSet para leer resultados
28. resultSet.next() para iterar filas
29. resultSet.getString(), getInt(), getDouble()
30. resultSet.getObject()
31. resultSet.getDate() y resultSet.getTimestamp()
32. resultSet.wasNull() para verificar nulls
33. ResultSetMetaData para información del ResultSet
34. getColumnCount(), getColumnName(), getColumnType()
35. DatabaseMetaData para información de la BD
36. Transactions con Connection
37. connection.setAutoCommit(false)
38. connection.commit() y connection.rollback()
39. Savepoints: connection.setSavepoint()
40. Transaction isolation levels
41. READ_UNCOMMITTED, READ_COMMITTED
42. REPEATABLE_READ, SERIALIZABLE
43. connection.setTransactionIsolation()
44. Batch operations con Statement
45. addBatch() y executeBatch()
46. Batch con PreparedStatement
47. Generated keys: getGeneratedKeys()
48. RETURN_GENERATED_KEYS
49. Scrollable ResultSet: TYPE_SCROLL_INSENSITIVE
50. Updatable ResultSet: CONCUR_UPDATABLE
51. RowSet: CachedRowSet, WebRowSet
52. RowSetFactory y RowSetProvider
53. DataSource interface (preferido sobre DriverManager)
54. JNDI lookup para DataSources
55. Connection pooling: DBCP, C3P0, HikariCP
56. HikariCP como el pool más rápido
57. Configuración de HikariCP en Spring Boot
58. Spring JdbcTemplate
59. JdbcTemplate.query() y JdbcTemplate.update()
60. RowMapper<T> para mapear ResultSet a objetos
61. BeanPropertyRowMapper<T>
62. NamedParameterJdbcTemplate
63. SqlParameterSource
64. SimpleJdbcInsert para INSERT simplificado
65. SQL fundamentals: SELECT, FROM, WHERE
66. SQL: ORDER BY, GROUP BY, HAVING
67. SQL: JOIN (INNER, LEFT, RIGHT, FULL)
68. SQL: Subqueries
69. SQL: CTEs (Common Table Expressions)
70. SQL: Window functions (ROW_NUMBER, RANK)
71. SQL: Aggregations (COUNT, SUM, AVG, MIN, MAX)
72. SQL: EXISTS e IN
73. SQL: INSERT, UPDATE, DELETE
74. SQL: CREATE TABLE, ALTER TABLE
75. SQL: Indexes y su impacto
76. SQL: Execution plans
77. Relational database design
78. Normalización: 1NF, 2NF, 3NF
79. Foreign keys y referential integrity
80. Primary keys: auto-increment vs UUID
81. Flyway para database migrations
82. Flyway: migrate(), info(), repair()
83. SQL migration files: V1__create_table.sql
84. Flyway en Spring Boot
85. Liquibase como alternativa a Flyway
86. Liquibase: changelogs en XML, YAML, SQL
87. Stored procedures vs dynamic SQL
88. Database views
89. Database triggers
90. Testing JDBC con H2 in-memory
91. Testcontainers para tests con BD real
92. Connection string en application.properties
93. Connection pooling y performance
94. Timeouts y retry policies
95. Database connection management best practices
96. Unit testing con base de datos in-memory
97. Integration testing con Docker (Testcontainers)
98. jOOQ como alternativa type-safe a JDBC
99. Spring Data JDBC como alternativa simplificada
100. Resumen: JDBC como base para entender ORMs

---

## MÓDULO 35: JPA / HIBERNATE - FUNDAMENTOS

**Descripción:** JPA (Jakarta Persistence API) es el estándar de persistencia de Java, e Hibernate es su implementación más popular. Aprenderás a mapear tablas a clases, a realizar CRUD, a configurar relaciones, a ejecutar migrations, y a escribir consultas JPQL.

1. ¿Qué es JPA y por qué usarlo?
2. ORM: Object-Relational Mapping
3. JPA como especificación, Hibernate como implementación
4. Code-First vs Database-First
5. Instalar Hibernate: hibernate-core y jakarta.persistence-api
6. EntityManager: el corazón de JPA
7. @Entity para marcar clases como entidades
8. @Table para nombre de tabla
9. @Id para clave primaria
10. @GeneratedValue para auto-generación (IDENTITY, SEQUENCE, AUTO)
11. @Column para configurar columnas
12. @Column(name, length, nullable, unique)
13. Tipos de datos y mapeo a SQL
14. String → VARCHAR
15. LocalDate → DATE
16. LocalDateTime → TIMESTAMP
17. BigDecimal → DECIMAL
18. @Enumerated(EnumType.STRING) para enums
19. @Lob para campos grandes (BLOB, CLOB)
20. @Transient para excluir del mapeo
21. @Access para controlar acceso (FIELD vs PROPERTY)
22. persistence.xml o Spring auto-config
23. application.properties: spring.jpa.* properties
24. spring.jpa.hibernate.ddl-auto: create, update, validate, none
25. EntityManagerFactory: crear EntityManagers
26. @PersistenceContext para inyectar EntityManager en Spring
27. Entity lifecycle: persist, merge, remove, find
28. entityManager.persist(entity) para INSERT
29. entityManager.find(Class, id) para SELECT por ID
30. entityManager.merge(entity) para UPDATE
31. entityManager.remove(entity) para DELETE
32. entityManager.flush() para sincronizar con BD
33. Entity states: New, Managed, Detached, Removed
34. Detached entities y reattachment con merge
35. JPQL: Java Persistence Query Language
36. @Query("SELECT e FROM Entity e WHERE ...")
37. entityManager.createQuery()
38. TypedQuery<T> con createQuery()
39. JPQL: SELECT, FROM, WHERE, ORDER BY
40. JPQL: JOIN (INNER JOIN, LEFT JOIN)
41. JPQL: FETCH JOIN para eager loading
42. JPQL: GROUP BY, HAVING
43. JPQL: Subqueries
44. Named queries: @NamedQuery
45. Native SQL queries: createNativeQuery()
46. @NamedNativeQuery
47. Relationships: @OneToMany
48. Relationships: @ManyToOne
49. @JoinColumn para foreign key
50. Relationships: @OneToOne
51. @OneToOne con mappedBy
52. Relationships: @ManyToMany
53. @JoinTable para tabla intermedia
54. Fetch types: EAGER vs LAZY
55. @OneToMany(fetch = FetchType.LAZY)
56. Eager loading: carga inmediata
57. Lazy loading: carga diferida
58. LazyInitializationException y cómo prevenirlo
59. @Transactional en Spring para sesiones
60. Open Session in View pattern (controversial)
61. EntityGraph para definir loading plans
62. @NamedEntityGraph
63. JPA callbacks: @PrePersist, @PostPersist
64. @PreUpdate, @PostUpdate
65. @PreRemove, @PostRemove
66. @PostLoad
67. @MappedSuperclass para herencia de campos
68. Inheritance strategies: SINGLE_TABLE
69. Inheritance: JOINED
70. Inheritance: TABLE_PER_CLASS
71. @DiscriminatorColumn y @DiscriminatorValue
72. Composite keys con @EmbeddedId
73. Composite keys con @IdClass
74. @Embeddable y @Embedded
75. Auditing con @CreatedDate, @LastModifiedDate
76. @CreatedBy, @LastModifiedBy
77. @EntityListeners y AuditingEntityListener
78. Spring Data JPA: JpaRepository<T, ID>
79. JpaRepository: findAll(), findById(), save()
80. JpaRepository: deleteById(), count(), existsById()
81. Custom queries con @Query en repositories
82. Derived queries: findByNombre(String nombre)
83. Query derivation: findByNombreAndEdad()
84. Pagination con Pageable y Page<T>
85. Sorting con Sort
86. Specifications con JpaSpecificationExecutor
87. Example queries con Query by Example
88. Projections con interfaces y clases
89. @Modifying para queries de UPDATE/DELETE
90. @Transactional en repositories
91. Flush mode: AUTO vs COMMIT
92. Batch fetching: @BatchSize
93. Second-level cache con EhCache o Hazelcast
94. @Cacheable en entidades
95. Caching strategies
96. N+1 problem: qué es y cómo resolverlo
97. Detectar N+1 con Hibernate logging
98. FETCH JOIN como solución
99. @BatchSize como solución
100. Resumen: flujo de trabajo de JPA/Hibernate

---

## MÓDULO 36: JPA / HIBERNATE - AVANZADO

**Descripción:** Este módulo profundiza en JPA/Hibernate para escenarios reales: performance optimization, interceptors, bulk operations, y patrones avanzados.

1. Hibernate properties avanzadas
2. hibernate.show_sql y hibernate.format_sql
3. hibernate.use_sql_comments
4. Statistics: hibernate.generate_statistics
5. Performance: batch size para inserts
6. hibernate.jdbc.batch_size
7. hibernate.order_inserts y order_updates
8. ID generation strategies en profundidad
9. IDENTITY vs SEQUENCE vs TABLE
10. UUID como primary key
11. Hibernate: @GenericGenerator
12. Sequences con @SequenceGenerator
13. Composite keys avanzados
14. @MapsId para shared primary keys
15. Orphan removal: @OneToMany(orphanRemoval = true)
16. Cascade types: ALL, PERSIST, MERGE, REMOVE
17. CascadeType.REFRESH, DETACH
18. Cuándo usar cada cascade type
19. Fetch profiles de Hibernate
20. @FetchProfile
21. Batch fetching strategies
22. Subselect fetching
23. Lazy property fetching: @LazyCollection
24. StatelessSession para bulk operations
25. ScrollableResults para procesar grandes resultados
26. DML-style operations: UPDATE con HQL
27. @Query con @Modifying para updates
28. Bulk delete con JPQL
29. Native queries para operaciones complejas
30. Stored procedures con JPA
31. @NamedStoredProcedureQuery
32. Result set mappings con @SqlResultSetMapping
33. @ConstructorResult para projections
34. Envers para auditoría (Hibernate Envers)
35. @Audited annotation
36. AuditReader para consultar historial
37. Revision types y revision entities
38. Filters de Hibernate: @Filter
39. Soft delete con @Filter
40. @Where para filtros estáticos
41. @Loader para custom SQL loading
42. Type converters con @Converter
43. AttributeConverter<X, Y>
44. Converter para enums personalizados
45. Converter para JSON fields
46. Converter para encriptación
47. @Formula para propiedades calculadas
48. @ColumnTransformer para transformaciones SQL
49. @Generated para valores generados por BD
50. Optimistic locking con @Version
51. OptimisticLockException handling
52. Pessimistic locking: LockModeType.PESSIMISTIC_READ
53. Pessimistic locking: PESSIMISTIC_WRITE
54. Lock timeouts
55. Multi-tenancy con Hibernate
56. Multi-tenant: DATABASE, SCHEMA, DISCRIMINATOR
57. CurrentTenantIdentifierResolver
58. MultiTenantConnectionProvider
59. Connection providers: HikariCP, C3P0
60. Second-level cache: EhCache 3
61. Hibernate caching regions
62. Query cache
63. Collection cache
64. Cache concurrency strategies
65. Testing JPA con @DataJpaTest
66. @AutoConfigureTestDatabase
67. H2 in-memory para tests
68. Testcontainers para PostgreSQL/MySQL tests
69. @Sql para scripts de test
70. @SqlGroup para múltiples scripts
71. Repository testing patterns
72. Integration tests con JPA
73. Performance tuning: batch fetching
74. Performance tuning: subselect fetching
75. Performance tuning: IDENTITY vs SEQUENCE
76. Performance tuning: dirty checking overhead
77. Performance tuning: bytecode enhancement
78. @DynamicInsert y @DynamicUpdate
79. Natural keys vs surrogate keys
80. Domain-Driven Design con JPA
81. Aggregate roots con JPA
82. Value objects con @Embeddable
83. DDD repositories con Spring Data
84. Specification pattern con JPA
85. CQRS: separate read and write
86. Read models con projections
87. Event sourcing con JPA (introducción)
88. JPA y records: limitaciones
89. JPA y sealed classes: limitaciones
90. Hibernate Reactive para non-blocking
91. Vert.x y Hibernate Reactive
92. Quarkus y Hibernate Reactive
93. jOOQ como alternativa a JPA para queries complejas
94. Spring Data JDBC como alternativa más simple
95. MyBatis como alternativa a JPA
96. JPA vs jOOQ vs MyBatis: comparativa
97. Database migrations con Flyway y JPA
98. hibernate.ddl-auto=validate en producción
99. JPA y virtual threads (Java 21)
100. Resumen: decisiones de diseño con JPA/Hibernate

---

## MÓDULO 37: SPRING BOOT - FUNDAMENTOS

**Descripción:** Spring Boot es el framework más popular para construir aplicaciones Java. Aprenderás auto-configuración, application properties, starters, web applications, REST APIs, y todo lo necesario para construir aplicaciones de producción con Spring Boot.

1. ¿Qué es Spring Boot y por qué dominar?
2. Spring Boot vs Spring Framework
3. Crear un proyecto: Spring Initializr
4. start.spring.io para generar proyecto
5. Estructura del proyecto generado
6. @SpringBootApplication: la anotación principal
7. @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan
8. SpringApplication.run(Application.class, args)
9. Auto-configuración: cómo funciona
10. spring-boot-autoconfigure module
11. @ConditionalOnClass, @ConditionalOnMissingBean
12. spring.factories / AutoConfiguration.imports
13. Starters: spring-boot-starter-web, starter-data-jpa
14. spring-boot-starter-test
15. spring-boot-starter-security
16. spring-boot-starter-actuator
17. spring-boot-starter-validation
18. application.properties
19. application.yml como alternativa
20. application-{profile}.properties
21. Server configuration: server.port, server.servlet.context-path
22. spring.datasource.* properties
23. spring.jpa.* properties
24. External configuration: environment variables
25. Command-line arguments
26. @Value para inyectar propiedades
27. @ConfigurationProperties para strong-typed
28. @EnableConfigurationProperties
29. Profiles: spring.profiles.active
30. @Profile("dev"), @Profile("prod")
31. YAML profiles en un solo archivo
32. Logging en Spring Boot: Logback default
33. logging.level.root=INFO
34. logging.level.com.example=DEBUG
35. logging.file.name=app.log
36. DevTools: auto-restart y live reload
37. spring-boot-devtools dependency
38. Packaging: executable JAR
39. java -jar application.jar
40. WAR deployment en Tomcat externo
41. spring-boot-maven-plugin
42. Embedded servers: Tomcat, Jetty, Undertow
43. Cambiar servidor embebido
44. Tomcat configuration
45. Error handling: /error endpoint
46. Custom error pages: error.html
47. ErrorController para custom error handling
48. Banner personalizado: banner.txt
49. SpringApplication.setBanner()
50. Listeners y Runners
51. ApplicationRunner para lógica post-startup
52. CommandLineRunner para argumentos
53. @Order para ordenar runners
54. ApplicationContext y beans disponibles
55. Graceful shutdown: server.shutdown=graceful
56. spring.lifecycle.timeout-per-shutdown-phase
57. Testing con @SpringBootTest
58. @SpringBootTest(webEnvironment = RANDOM_PORT)
59. TestRestTemplate para testear endpoints
60. MockMvc para testear controllers
61. @WebMvcTest para tests de controller
62. @DataJpaTest para tests de repository
63. @TestConfiguration para beans de test
64. Actuator endpoints: /actuator/health, /actuator/info
65. management.endpoints.web.exposure.include=*
66. Custom actuator endpoints
67. Metrics con Actuator
68. Micrometer integration
69. Spring Boot y Docker
70. Dockerfile con Spring Boot
71. layered JARs para Docker cache
72. Cloud Native Buildpacks: spring-boot:build-image
73. GraalVM Native Image con Spring Boot
74. spring-boot-starter-parent como parent POM
75. Dependency management con Spring Boot BOM
76. Overrides de versiones de dependencias
77. Multi-module Spring Boot projects
78. Spring Boot CLI (raramente usado)
79. Spring Boot y Kotlin
80. Spring Boot y virtual threads (3.2+)
81. spring.threads.virtual.enabled=true
82. Spring Boot y records
83. Spring Boot y sealed classes
84. Spring Boot y Java 21 features
85. Spring Boot DevTools en producción (nunca)
86. Security básico: spring-boot-starter-security
87. Default login con Spring Security
88. Custom security configuration
89. Spring Boot Actuator security
90. CORS configuration en Spring Boot
91. Async processing: @EnableAsync y @Async
92. Scheduling: @EnableScheduling y @Scheduled
93. @Scheduled(fixedRate, fixedDelay, cron)
94. Executor configuration para async
95. Spring Cache: @EnableCaching, @Cacheable
96. Cache providers: Caffeine, Redis, EhCache
97. @CacheEvict, @CachePut
98. Spring Boot y Kafka (introducción)
99. Spring Boot y RabbitMQ (introducción)
100. Resumen: checklist de una aplicación Spring Boot

---

## MÓDULO 38: SPRING MVC Y REST APIs

**Descripción:** Spring MVC es el framework web de Spring. Aprenderás a crear controllers, endpoints REST, manejar requests y responses, validación, error handling, documentación con OpenAPI, y versioning de APIs.

1. ¿Qué es Spring MVC?
2. El modelo: DispatcherServlet → Handler → Controller
3. @RestController para APIs REST
4. @Controller para MVC con vistas
5. @RequestMapping para mapear URLs
6. @GetMapping, @PostMapping, @PutMapping
7. @DeleteMapping, @PatchMapping
8. @PathVariable para parámetros de URL
9. @RequestParam para query parameters
10. @RequestBody para body JSON
11. @ResponseBody (implícito en @RestController)
12. ResponseEntity<T> para respuestas con status
13. ResponseEntity.ok(), ResponseEntity.notFound()
14. ResponseEntity.created(), ResponseEntity.noContent()
15. ResponseEntity.status(HttpStatus.CREATED)
16. Content negotiation: Accept header
17. Produces y Consumes en mappings
18. @RequestMapping(produces = "application/json")
19. Validación con Jakarta Validation
20. @Valid en @RequestBody
21. @NotNull, @NotEmpty, @NotBlank
22. @Size(min, max)
23. @Min, @Max, @Positive
24. @Email, @Pattern
25. @Validated en el controller
26. BindingResult para errores de validación
27. @ExceptionHandler en controller
28. @ControllerAdvice para manejo global de errores
29. @RestControllerAdvice
30. ResponseEntityExceptionHandler
31. Custom exception classes
32. Error response con ProblemDetail (Spring 6)
33. Error response con ErrorResponse
34. DTOs para request y response
35. ModelMapper o MapStruct para mapping
36. Pagination: Pageable y Page<T>
37. @PageableDefault para defaults
38. PagedModel de Spring HATEOAS
39. Sorting: Sort.by("field")
40. Filtering con Specifications
41. API versioning: URI versioning
42. Header versioning
43. Media type versioning
44. @ApiVersion custom annotation
45. OpenAPI / Swagger con springdoc-openapi
46. springdoc-openapi-starter-webmvc-ui
47. /swagger-ui/index.html
48. @Operation(summary, description)
49. @ApiResponse(responseCode, description)
50. @Tag para agrupar endpoints
51. @Schema para documentar modelos
52. @Parameter para documentar parámetros
53. Security en REST APIs
54. CORS: @CrossOrigin
55. WebMvcConfigurer.addCorsMappings()
56. Global CORS con @Configuration
57. Rate limiting con Bucket4j
58. ETag y conditional requests
59. Cache-Control headers
60. HATEOAS con Spring HATEOAS
61. EntityModel, CollectionModel
62. WebMvcLinkBuilder
63. Self-descriptive APIs
64. Hypermedia como engine (HATEOAS)
65. File upload: @RequestParam MultipartFile
66. Múltiples archivos: List<MultipartFile>
67. File download: ResponseEntity<Resource>
68. StreamingResponseBody para archivos grandes
69. Async endpoints: Callable<T>, DeferredResult<T>
70. Streaming con SSE (Server-Sent Events)
71. SseEmitter para eventos de servidor
72. WebClient como alternativa a RestTemplate
73. RestTemplate (legacy) para HTTP clients
74. WebClient (reactive) para HTTP clients
75. HttpClient de Java 11+ como alternativa
76. Interceptors: HandlerInterceptor
77. Filter vs Interceptor en Spring
78. OncePerRequestFilter
79. Logging filter para requests/responses
80. Correlation ID filter
81. Transaction management: @Transactional
82. Propagation: REQUIRED, REQUIRES_NEW, NESTED
83. Isolation levels en @Transactional
84. Rollback rules: rollbackFor
85. Read-only transactions: @Transactional(readOnly = true)
86. Testing REST APIs
87. @WebMvcTest con MockMvc
88. mockMvc.perform(get("/api/users"))
89. mockMvc.andExpect(status().isOk())
90. mockMvc.andExpect(jsonPath("$[0].name").value("Ana"))
91. @SpringBootTest con TestRestTemplate
92. WebTestClient para tests reactivos
93. MockMvc con @AutoConfigureMockMvc
94. JSON path assertions
95. Integration tests con real server
96. WireMock para mock de APIs externas
97. Contract testing con Spring Cloud Contract
98. REST API best practices
99. Richardson Maturity Model
100. Resumen: diseño de APIs REST profesionales

---

## MÓDULO 39: SPRING SECURITY

**Descripción:** La seguridad es crítica en cualquier aplicación. Aprenderás autenticación y autorización con Spring Security, JWT tokens, OAuth2, method-level security, y las mejores prácticas de seguridad web.

1. ¿Qué es Spring Security?
2. SecurityFilterChain: el pipeline de seguridad
3. @EnableWebSecurity
4. SecurityFilterChain bean en configuración
5. @Configuration con @Bean SecurityFilterChain
6. authorizeHttpRequests() para autorizar URLs
7. requestMatchers("/api/**").authenticated()
8. requestMatchers("/public/**").permitAll()
9. anyRequest().authenticated()
10. Form login: formLogin()
11. HTTP Basic: httpBasic()
12. CSRF protection: csrf()
13. CORS en Spring Security
14. Session management: sessionManagement()
15. Stateless sessions para APIs
16. UserDetailsService interface
17. UserDetails para representar usuario
18. InMemoryUserDetailsManager
19. JdbcUserDetailsManager
20. Custom UserDetailsService con JPA
21. Password encoding: BCryptPasswordEncoder
22. PasswordEncoder interface
23. DelegatingPasswordEncoder
24. NoOpPasswordEncoder (solo para tests)
25. AuthenticationManager
26. AuthenticationProvider
27. Authentication object
28. SecurityContextHolder y SecurityContext
29. @AuthenticationPrincipal para obtener usuario
30. JWT authentication
31. Crear JWT tokens con jjwt library
32. JwtDecoder y JwtEncoder
33. AuthenticationFilter para JWT
34. OncePerRequestFilter para JWT
35. Extraer token del header Authorization
36. Validar token y crear Authentication
37. JWT refresh token pattern
38. OAuth2 con Spring Security
39. spring-boot-starter-oauth2-resource-server
40. spring-boot-starter-oauth2-client
41. OAuth2 login con Google, GitHub
42. @EnableOAuth2Client
43. OAuth2 authorization code flow
44. OAuth2 client credentials flow
45. OIDC (OpenID Connect) support
46. Method-level security
47. @EnableMethodSecurity
48. @PreAuthorize("hasRole('ADMIN')")
49. @PreAuthorize con SpEL
50. @PostAuthorize para post-ejecución
51. @Secured("ROLE_ADMIN")
52. @RolesAllowed("ADMIN")
53. Security con expression-based access
54. hasRole(), hasAuthority()
55. hasAnyRole(), hasAnyAuthority()
56. isAnonymous(), isAuthenticated()
57. Custom permission evaluator
58. ACL (Access Control Lists)
59. Method security y AOP
60. Security en tests
61. @WithMockUser para tests
62. @WithUserDetails
63. SecurityMockMvcRequestPostProcessors.jwt()
64. MockMvc con autenticación
65. API key authentication
66. Custom authentication filter
67. Custom success/failure handlers
68. Remember-me authentication
69. Concurrent session control
70. Session fixation protection
71. Security headers: Content-Security-Policy
72. X-Content-Type-Options
73. X-Frame-Options
74. Strict-Transport-Security
75. Referrer-Policy
76. OWASP Top 10 y Spring Security
77. SQL injection prevention (JPA/PreparedStatement)
78. XSS prevention (encoding automático)
79. CSRF protection en Spring MVC
80. Rate limiting con Bucket4j + Spring Security
81. Brute force protection
82. Account lockout
83. Security logging y auditing
84. @PreFilter y @PostFilter para filtrar colecciones
85. SecurityConfig patterns
86. Multiple SecurityFilterChains
87. SecurityMatcher para filtrar cadenas
88. Lambda DSL en Spring Security 6
89. Obsolete: WebSecurityConfigurerAdapter (no usar)
90. Spring Security y virtual threads
91. Spring Security y OAuth2 Resource Server
92. JWT validation con issuer-uri
93. Claim-based authorization
94. Custom JWT claims
95. Spring Authorization Server
96. Crear un Authorization Server propio
97. Token introspection
98. Token revocation
99. Fine-grained authorization con OPA (Open Policy Agent)
100. Resumen: checklist de seguridad para producción

---

## MÓDULO 40: SPRING WEBFLUX Y PROGRAMACIÓN REACTIVA

**Descripción:** Spring WebFlux permite construir aplicaciones web reactivas y no bloqueantes. Aprenderás Project Reactor (Flux y Mono), WebClient, routers, y los casos de uso donde la programación reactiva es beneficiosa.

1. ¿Qué es programación reactiva?
2. Reactive Manifesto: responsive, resilient, elastic, message-driven
3. Spring WebFlux vs Spring MVC
4. Blocking vs non-blocking I/O
5. Reactor Netty como servidor embebido
6. Project Reactor: Flux y Mono
7. Flux<T>: 0 a N elementos
8. Mono<T>: 0 a 1 elemento
9. Crear Flux: Flux.just(), Flux.fromIterable()
10. Crear Flux: Flux.range(), Flux.interval()
11. Crear Mono: Mono.just(), Mono.empty()
12. Crear Mono: Mono.fromCallable(), Mono.fromFuture()
13. Operadores de transformación: map(), flatMap()
14. Operadores de filtrado: filter(), distinct()
15. Operadores de combinación: merge(), zip(), concat()
16. Operadores de error: onErrorReturn(), onErrorResume()
17. Operadores de retry: retry(), retryWhen()
18. Schedulers: boundedElastic(), parallel(), single()
19. subscribeOn() y publishOn()
20. Backpressure: gestión de demanda
21. Backpressure strategies: BUFFER, DROP, LATEST, ERROR
22. Flux.onBackpressureBuffer(), onBackpressureDrop()
23. Flux.create() y Flux.push() para programmatic creation
24. Sinks en Reactor 3
25. Sinks.many().multicast() para hot/cold
26. Cold vs Hot publishers
27. StepVerifier para testing de Reactor
28. StepVerifier.create(flux).expectNext().verifyComplete()
29. WebFlux Router Functions
30. RouterFunction<ServerResponse>
31. RouterFunctions.route() con RequestPredicate
32. HandlerFunction para procesar requests
33. Functional endpoints vs annotated controllers
34. @RestController en WebFlux
35. @GetMapping con Mono y Flux como retorno
36. @RequestBody Mono<T>
37. ResponseEntity<Mono<T>> y ResponseEntity<Flux<T>>
38. WebClient para HTTP reactivo
39. WebClient.create("http://api.example.com")
40. webClient.get().uri("/users").retrieve()
41. WebClient con bodyToFlux() y bodyToMono()
42. WebClient con exchange() para control total
43. WebClient filters para logging, auth
44. WebClient error handling
45. ServerHttpRequest y ServerHttpResponse
46. WebFilter para filtros reactivos
47. Reactive Security con Spring Security WebFlux
48. SecurityWebFilterChain
49. ReactiveUserDetailsService
50. JWT en WebFlux
51. Reactive Data Access: R2DBC
52. R2DBC: Reactive Relational Database Connectivity
53. R2DBC Repository: ReactiveCrudRepository
54. Flux<User> findAll()
55. Mono<User> findById()
56. DatabaseClient para queries manuales
57. R2DBC con H2, PostgreSQL, MySQL
58. spring-boot-starter-data-r2dbc
59. Reactive MongoDB con spring-boot-starter-data-mongodb-reactive
60. ReactiveRedisTemplate para Redis
61. Server-Sent Events (SSE) en WebFlux
62. Flux<ServerSentEvent> para streaming
63. WebSocket en WebFlux
64. WebSocketHandler
65. Reactive WebSocket
66. Testing WebFlux controllers
67. WebTestClient para tests
68. webClient.get().uri("/api/users").exchange()
69. .expectStatus().isOk().expectBody()
70. Testing R2DBC repositories
71. Cuándo usar WebFlux vs MVC
72. WebFlux: I/O bound, high concurrency
73. MVC + virtual threads como alternativa moderna
74. Virtual threads vs reactive: comparativa
75. WebFlux y virtual threads (no directamente)
76. RSocket como protocolo reactivo
77. Spring Messaging con RSocket
78. Reactor debugging: Hooks.onOperatorDebug()
79. Reactor debugging con checkpoint()
80. Memory leaks en reactive programming
81. Subscription leaks
82. Reactor Extras: Flux.compose()
83. StepVerifier con VirtualTime
84. Testing con StepVerifier: expectNextCount()
85. WebFlux y Micrometer metrics
86. WebFlux y distributed tracing
87. WebFlux en microservices
88. API Gateway con Spring Cloud Gateway (reactive)
89. Circuit Breaker con Resilience4j
90. Retry con Resilience4j
91. Rate limiter con Resilience4j
92. Bulkhead con Resilience4j
93. WebFlux y Kotlin coroutines
94. Kotlin Flow y Reactor interop
95. WebFlux performance benchmarks
96. WebFlux en containers Docker
97. GraalVM Native Image y WebFlux
98. WebFlux y Spring Boot Actuator
99. WebFlux y gRPC (reactive)
100. Resumen: reactive vs imperative en el ecosistema Spring

---

## MÓDULO 41: TESTING - JUNIT 5, MOCKITO Y TDD

**Descripción:** El testing es lo que separa el código profesional del amateur. Aprenderás JUnit 5, Mockito, integration testing, TDD, y cómo medir cobertura de código.

1. ¿Por qué testear software?
2. Tipos de tests: Unit, Integration, E2E
3. Testing pyramid
4. Arrange, Act, Assert (AAA pattern)
5. JUnit 5: el framework de testing de Java
6. Crear un proyecto con junit-jupiter
7. @Test para tests individuales
8. @DisplayName para nombres legibles
9. Assertions: assertEquals, assertNotEquals
10. Assertions: assertTrue, assertFalse
11. Assertions: assertNull, assertNotNull
12. Assertions: assertThrows para excepciones
13. Assertions: assertAll para múltiples assertions
14. Assertions: assertTimeout para timeouts
15. Assertions: assertIterableEquals para colecciones
16. Assertions: assertLinesMatch para strings
17. @ParameterizedTest para tests parametrizados
18. @ValueSource(ints = {1, 2, 3})
19. @ValueSource(strings = {"a", "b"})
20. @CsvSource para datos CSV
21. @CsvFileSource para archivo CSV
22. @MethodSource para datos de método
23. @EnumSource para datos de enum
24. @ArgumentsSource para custom provider
25. @BeforeEach para setup por test
26. @AfterEach para cleanup por test
27. @BeforeAll para setup de clase (static)
28. @AfterAll para cleanup de clase (static)
29. @TestInstance(Lifecycle.PER_CLASS)
30. Test lifecycle en JUnit 5
31. @Nested para tests anidados
32. @Tag para categorizar tests
33. @Disabled para deshabilitar tests
34. @RepeatedTest para tests repetidos
35. @TestFactory para tests dinámicos
36. DynamicTest.generate()
37. Extension Model de JUnit 5
38. @ExtendWith para extensiones
39. BeforeEachCallback, AfterEachCallback
40. TestWatcher para observar resultados
41. Mockito: framework de mocking
42. @Mock para crear mocks
43. @InjectMocks para inyectar mocks
44. @ExtendWith(MockitoExtension.class)
45. Mockito.when(mock.method()).thenReturn(value)
46. Mockito.when(...).thenThrow(exception)
47. Mockito.verify(mock).method()
48. Mockito.verify(mock, times(1)).method()
49. Mockito.verify(mock, never()).method()
50. Mockito.verify(mock, atLeast(1)).method()
51. ArgumentMatchers: any(), anyString(), anyInt()
52. ArgumentMatchers: eq(), isNull(), notNull()
53. ArgumentCaptor para capturar argumentos
54. Mockito.doNothing().when(mock).voidMethod()
55. Mockito.doThrow().when(mock).voidMethod()
56. Mockito.doReturn().when(mock) (avoid)
57. Spy: partial mocking con @Spy
58. Mockito.reset(mock) para resetear
59. BDD style: given().willReturn()
60. BDD style: then(mock).should()
61. @MockitoSettings(strictness = Strictness.STRICT_STUBS)
62. UnnecessaryStubbingException
63. MissingInvocationException
64. TDD: Test-Driven Development
65. Red → Green → Refactor
66. Escribir el test primero (Red)
67. Código mínimo para pasar (Green)
68. Refactorizar manteniendo tests verdes
69. TDD example: calculadora
70. TDD example: validación de email
71. TDD example: String kata
72. Outside-in TDD
73. Inside-out TDD
74. Integration tests con @SpringBootTest
75. @SpringBootTest(webEnvironment = RANDOM_PORT)
76. TestRestTemplate
77. MockMvc para tests de controller
78. @WebMvcTest con MockMvc
79. @DataJpaTest para tests de repository
80. @JdbcTest para tests de JDBC
81. H2 in-memory database para tests
82. @Sql para scripts de setup
83. Testcontainers para base de datos real
84. @Testcontainers annotation
85. PostgreSQLContainer para PostgreSQL
86. GenericContainer para otros servicios
87. WireMock para mock de APIs HTTP
88. @WireMockTest
89. MockWebServer de OkHttp
90. Test doubles: Dummy, Stub, Mock, Fake, Spy
91. Cobertura de código: JaCoCo
92. jacoco-maven-plugin
93. jacoco:report para reportes HTML
94. Cobertura objetivo: 80%+
95. Branch coverage vs line coverage
96. Mutation testing con PIT (pitest)
97. pitest: mutar código y verificar tests
98. Mutation score como métrica
99. Naming conventions para tests
100. Resumen: estrategia de testing para un proyecto real

---

## MÓDULO 42: PRINCIPIOS SOLID, PATRONES DE DISEÑO Y CLEAN CODE

**Descripción:** Los principios SOLID y los patrones de diseño son la base del código mantenible y escalable. Aprenderás los cinco principios SOLID aplicados a Java, los patrones GoF más utilizados, y arquitectura limpia.

1. Clean Code de Robert C. Martin
2. Nombres significativos
3. Funciones pequeñas
4. Comentarios: cuándo sí y cuándo no
5. DRY: Don't Repeat Yourself
6. KISS: Keep It Simple, Stupid
7. YAGNI: You Aren't Gonna Need It
8. Single Responsibility Principle (SRP)
9. Open/Closed Principle (OCP)
10. Liskov Substitution Principle (LSP)
11. Interface Segregation Principle (ISP)
12. Dependency Inversion Principle (DIP)
13. Strategy Pattern
14. Observer Pattern
15. Decorator Pattern
16. Factory Method Pattern
17. Abstract Factory Pattern
18. Singleton Pattern
19. Builder Pattern
20. Repository Pattern
21. Unit of Work Pattern
22. Command Pattern
23. CQRS Pattern
24. Mediator Pattern (MediatR en Java)
25. Chain of Responsibility
26. Adapter Pattern
27. Façade Pattern
28. Composite Pattern
29. Template Method Pattern
30. State Pattern
31. Specification Pattern
32. Null Object Pattern
33. Circuit Breaker Pattern
34. Retry Pattern
35. Cache-Aside Pattern
36. Event Sourcing (concepto)
37. Clean Architecture
38. Domain, Application, Infrastructure, Presentation
39. Vertical Slice Architecture
40. Hexagonal Architecture
41. Arquitectura modular
42. Domain-Driven Design (DDD)
43. Entities vs Value Objects
44. Aggregates y Aggregate Roots
45. Domain Events
46. Bounded Contexts
47. Ubiquitous Language
48. Anti-corruption Layer
49. Context Mapping
50. Resumen: aplicar principios sin over-engineering

---

## MÓDULO 43: SPRING DATA Y ACCESO A DATOS MODERNO

**Descripción:** Spring Data simplifica enormemente el acceso a datos. Aprenderás Spring Data JPA, Spring Data JDBC, Spring Data MongoDB, Spring Data Redis, y patrones avanzados como Specifications, QueryDSL, y projections.

1. Spring Data umbrella project
2. Spring Data JPA revisión
3. JpaRepository<T, ID>
4. Derived query methods
5. @Query con JPQL y native SQL
6. @Modifying queries
7. Pagination y Sorting
8. Specifications con JpaSpecificationExecutor
9. Specification<T> interface
10. Root, CriteriaQuery, CriteriaBuilder
11. Componer specifications con and(), or()
12. Query by Example (QBE)
13. ExampleMatcher para configurar matching
14. Projections: interface-based
15. Projections: class-based (DTOs)
16. Closed projections (solo getters de campos)
17. Open projections (con @Value y SpEL)
18. Dynamic projections
19. Custom repository implementations
20. Repository fragment pattern
21. @NoRepositoryBean para repositorio base
22. Auditing con @EnableJpaAuditing
23. @CreatedDate, @LastModifiedDate
24. @CreatedBy con AuditorAware
25. Spring Data JDBC como alternativa más simple
26. Spring Data JDBC: Aggregate root concept
27. SpringDataJdbcRepository
28. Spring Data MongoDB
29. MongoTemplate y MongoRepository
30. @Document annotation
31. Mongo queries con @Query
32. Spring Data Redis
33. RedisTemplate y StringRedisTemplate
34. @RedisHash para entities
35. Redis repositories
36. Spring Data Elasticsearch
37. ElasticsearchOperations y ElasticsearchRepository
38. Spring Data R2DBC (reactive)
39. ReactiveCrudRepository
40. DatabaseClient para queries manuales
41. Spring Data Neo4j
42. Spring Data Cassandra
43. Multi-datasource configuration
44. @Primary y @Qualifier para múltiples DataSources
45. AbstractRoutingDataSource para dynamic routing
46. Read-write splitting
47. CQRS con Spring Data
48. jOOQ integration con Spring
49. jOOQ: type-safe SQL queries
50. DSLContext para queries jOOQ
51. Resumen: cuándo usar qué herramienta de datos

---

## MÓDULO 44: MICROSERVICIOS CON SPRING CLOUD

**Descripción:** Los microservicios son la arquitectura dominante para sistemas grandes. Aprenderás Spring Cloud para service discovery, configuration, API gateway, circuit breaker, y distributed tracing.

1. ¿Qué son los microservicios?
2. Monolito vs microservicios
3. Spring Cloud: overview
4. Service Discovery con Eureka
5. Eureka Server para registro de servicios
6. Eureka Client para registrarse
7. @EnableDiscoveryClient
8. DiscoveryClient para buscar servicios
9. Load balancing con Spring Cloud LoadBalancer
10. @LoadBalanced en RestTemplate/WebClient
11. Service discovery con Consul
12. Service discovery con Kubernetes
13. Configuration Server con Spring Cloud Config
14. Config Server para configuración centralizada
15. Git-based configuration
16. @RefreshScope para recargar config
17. Bus para refresh masivo: Spring Cloud Bus
18. API Gateway con Spring Cloud Gateway
19. Route predicates
20. Gateway filters
21. Rate limiting en Gateway
22. Authentication en Gateway
23. Circuit Breaker con Resilience4j
24. @CircuitBreaker annotation
25. Circuit states: CLOSED, OPEN, HALF_OPEN
26. Fallback methods
27. Bulkhead con Resilience4j
28. Rate limiter con Resilience4j
29. Retry con Resilience4j
30. Time limiter con Resilience4j
31. Distributed tracing con Micrometer Tracing
32. Trace propagation entre servicios
33. Centralized logging con ELK
34. OpenTelemetry para tracing
35. Spring Cloud Stream para messaging
36. Kafka binder
37. RabbitMQ binder
38. Event-driven microservices
39. Saga pattern
40. Choreography-based saga
41. Orchestration-based saga
42. CQRS en microservicios
43. Event sourcing con Kafka
44. API composition pattern
45. Database per service
46. Shared database anti-pattern
47. Service mesh (introducción)
48. Istio y Linkerd
49. Kubernetes y microservicios
50. Resumen: decisiones de arquitectura

---

## MÓDULO 45: MESSAGING Y EVENT-DRIVEN ARCHITECTURE

**Descripción:** Los sistemas basados en mensajes son fundamentales para arquitecturas desacopladas. Aprenderás JMS, Kafka, RabbitMQ, y los patrones de mensajería que se usan en sistemas de producción.

1. ¿Qué es messaging?
2. Point-to-point vs Publish-subscribe
3. JMS (Java Message Service)
4. JMS: Queue y Topic
5. JMS: MessageProducer y MessageConsumer
6. TextMessage, ObjectMessage, MapMessage
7. ActiveMQ como broker JMS
8. Jakarta Messaging API
9. Apache Kafka: ¿Qué es?
10. Kafka: Topics, Partitions, Offsets
11. Kafka: Producers y Consumers
12. Kafka: Consumer Groups
13. spring-kafka: Spring Boot starter
14. KafkaTemplate para enviar mensajes
15. @KafkaListener para recibir mensajes
16. Kafka serializers/deserializers
17. Avro schemas con Schema Registry
18. Kafka Streams para procesamiento de streams
19. Kafka Connect para integración
20. Exactly-once semantics
21. At-least-once vs at-most-once
22. RabbitMQ: ¿Qué es?
23. AMQP protocol
24. RabbitMQ: Exchanges, Queues, Bindings
25. Direct, Topic, Fanout, Headers exchanges
26. spring-amqp: Spring Boot starter
27. RabbitTemplate para enviar
28. @RabbitListener para recibir
29. Dead letter queues
30. Message acknowledgment
31. Spring Cloud Stream abstraction
32. @EnableBinding (legacy) o functional model
33. spring.cloud.stream.bindings
34. Event-driven architecture patterns
35. Event notification
36. Event-carried state transfer
37. Event sourcing
38. CQRS con eventos
39. Saga pattern con messaging
40. Transactional outbox pattern
41. Idempotent consumers
42. Message deduplication
43. Schema evolution
44. CloudEvents specification
45. Testing messaging systems
46. Embedded Kafka para tests
47. Testcontainers para Kafka/RabbitMQ
48. Message ordering guarantees
49. Partitioning strategies
50. Resumen: cuándo usar qué sistema de mensajería

---

## MÓDULO 46: WEBSOCKETS Y COMUNICACIÓN EN TIEMPO REAL

**Descripción:** Las aplicaciones modernas necesitan comunicación bidireccional en tiempo real. Aprenderás WebSockets con Spring, Server-Sent Events, y los patrones de comunicación en tiempo real.

1. HTTP polling vs WebSockets vs SSE
2. WebSockets: protocolo bidireccional
3. WebSocket support en Spring
4. @EnableWebSocket
5. WebSocketHandler interface
6. TextWebSocketHandler
7. BinaryWebSocketHandler
8. WebSocketConfigurer para registrar handlers
9. STOMP sobre WebSocket
10. @EnableWebSocketMessageBroker
11. SimpMessagingTemplate para enviar mensajes
12. @MessageMapping para mapear endpoints
13. @SendTo para enviar a destinos
14. @SubscribeMapping para suscripciones
15. SockJS como fallback
16. StompHeaders y StompSession
17. Message Broker: simple broker vs external
18. External broker con RabbitMQ
19. External broker con Kafka
20. Authentication en WebSockets
21. ChannelInterceptor para auth
22. User destinations: /user/queue/notifications
23. convertAndSendToUser()
24. Chat application con STOMP
25. Notificaciones en tiempo real
26. Dashboard en tiempo real
27. Collaborative editing con WebSockets
28. Server-Sent Events (SSE) en Spring MVC
29. SseEmitter para enviar eventos
30. StreamingResponseBody
31. TextEventStream
32. SSE vs WebSockets: cuándo usar cada uno
33. WebSocket testing
34. Integration tests con WebSocket
35. WebSocket y virtual threads
36. Scaling WebSockets con Redis pub/sub
37. Scaling WebSockets con Kafka
38. Connection management y tracking
39. Heartbeat y keepalive
40. Reconnection strategies
41. WebSocket y Spring Security
42. WebSocket y Spring Cloud
43. RSocket como alternativa
44. RSocket: fire-and-forget, request-stream
45. gRPC streaming para comunicación
46. Long polling como alternativa legacy
47. WebTransport (futuro)
48. Client-side WebSocket en Java
49. Java WebSocket API (JSR 356 / Jakarta WebSocket)
50. Resumen: cuándo usar WebSockets vs SSE vs polling

---

## MÓDULO 47: DOCKER, KUBERNETES Y DESPLIEGUE

**Descripción:** El último módulo técnico te prepara para llevar tu código a producción. Aprenderás containerización con Docker, orquestación con Kubernetes, pipelines de CI/CD, y despliegue en cloud.

1. ¿Qué es Docker y por qué usarlo?
2. Contenedores vs Máquinas Virtuales
3. Dockerfile para aplicaciones Java
4. FROM eclipse-temurin:21-jre
5. COPY, WORKDIR, EXPOSE, ENTRYPOINT
6. Multi-stage builds en Dockerfile
7. FROM maven:3.9-eclipse-temurin-21 AS build
8. Build image: docker build -t miapp .
9. Run container: docker run -p 8080:8080 miapp
10. Docker Compose para multi-container
11. docker-compose.yml: app + database + cache
12. Environment variables en Docker
13. Docker secrets
14. Docker health checks
15. .dockerignore
16. Image size optimization
17. Jib plugin de Google para Docker sin Dockerfile
18. spring-boot-maven-plugin: build-image
19. Cloud Native Buildpacks
20. GraalVM Native Image para containers pequeños
21. Kubernetes basics
22. Pods, Services, Deployments
23. kubectl apply -f deployment.yaml
24. Kubernetes YAML para Spring Boot
25. ConfigMap y Secrets en Kubernetes
26. Horizontal Pod Autoscaler
27. Liveness y Readiness probes
28. Service types: ClusterIP, NodePort, LoadBalancer
29. Ingress controller
30. Helm charts
31. GitHub Actions para CI/CD
32. .github/workflows/ci.yml
33. actions/checkout, actions/setup-java
34. mvn clean install, mvn test
35. Docker build y push en pipeline
36. Deploy a Kubernetes con pipeline
37. GitOps con ArgoCD
38. Deploy a AWS ECS
39. Deploy a Google Cloud Run
40. Deploy a Azure Container Apps
41. AWS Lambda con GraalVM Native Image
42. Blue-green deployment
43. Canary deployment
44. Rolling updates
45. Feature flags para deploy seguro
46. Infrastructure as Code: Terraform
47. Pulumi con Java
48. Monitoring en producción
49. Alerting y runbooks
50. Resumen: checklist de producción para una app Java

---

## MÓDULO 48: LIBRERÍAS ESENCIALES DEL ECOSISTEMA JAVA

**Descripción:** El ecosistema Java tiene librerías que todo desarrollador profesional debe conocer. Aprenderás las más importantes: Lombok, MapStruct, Guava, Apache Commons, Resilience4j, Vavr, y más.

1. Project Lombok: reducir boilerplate
2. @Getter, @Setter, @ToString, @EqualsAndHashCode
3. @Data (combina lo anterior)
4. @Value para clases inmutables
5. @Builder para patrón builder
6. @AllArgsConstructor, @NoArgsConstructor
7. @RequiredArgsConstructor
8. @Slf4j para logger automático
9. @Cleanup para recursos
10. @SneakyThrows para checked exceptions
11. Lombok y records: ¿cuándo usar cada uno?
12. MapStruct: mapeo compile-time
13. @Mapper annotation
14. Mapping entre DTOs y entidades
15. @Mapping para custom mappings
16. Múltiples sources/targets
17. MapStruct vs ModelMapper
18. Google Guava: utilidades
19. Immutable collections: ImmutableList, ImmutableMap
20. Preconditions: checkArgument, checkState
21. Strings: nullToEmpty, emptyToNull
22. Collections2, Lists, Maps, Sets
23. Multimap, Multiset, BiMap, Table
24. Optional (Guava version)
25. Cache: LoadingCache, CacheBuilder
26. EventBus
27. Apache Commons Lang
28. StringUtils: isBlank, capitalize, abbreviate
29. ObjectUtils: defaultIfNull
30. Pair, Triple
31. EqualsBuilder, HashCodeBuilder
32. ToStringBuilder
33. Apache Commons IO
34. FileUtils: readFileToString, writeStringToFile
35. IOUtils: copy, toString
36. Apache Commons Collections
37. Bag, BidiMap, OrderedMap
38. Resilience4j: tolerancia a fallos
39. CircuitBreaker, Retry, RateLimiter
40. Bulkhead, TimeLimiter
41. Vavr: programación funcional
42. Either, Try, Option, Future
43. List, Map, Set de Vavr
44. Pattern matching con Vavr
45. Jackson: el serializador JSON más usado
46. Gson: alternativa de Google
47. OkHttp: cliente HTTP
48. Retrofit: HTTP client declarativo
49. WireMock: mock de HTTP
50. Resumen: toolkit esencial del desarrollador Java

---

## MÓDULO 49: JAVA MODERNO (JAVA 17-21) Y TENDENCIAS

**Descripción:** Java ha evolucionado enormemente. Aprenderás las características más recientes, las tendencias del ecosistema, GraalVM, y el futuro de Java.

1. Java release cadence: cada 6 meses
2. LTS releases: 8, 11, 17, 21
3. Features de Java 17
4. Sealed classes (final)
5. Pattern matching for instanceof (final)
6. Strong encapsulation de JDK internals
7. Features de Java 21
8. Virtual threads (final)
9. Pattern matching for switch (final)
10. Record patterns (final)
11. Sequenced collections
12. String templates (preview)
13. Unnamed patterns and variables
14. Scoped values (preview)
15. Structured concurrency (preview)
16. Foreign Function & Memory API (final)
17. ZGC generational
18. Key encapsulation mechanism API
19. Project Loom: virtual threads
20. Project Panama: foreign function
21. Project Valhalla: value types
22. Project Amber: language features
23. Project CracCoordinated Restore at Checkpoint)
24. GraalVM: polyglot VM
25. GraalVM Native Image
26. AOT compilation con GraalVM
27. Reflection limits en GraalVM
28. Quarkus framework con GraalVM
29. Micronaut framework
30. Spring Boot con GraalVM
31. Leyden Project: startup optimization
32. Vector API (incubator)
33. Foreign Function & Memory API
34. Panama: acceso a memoria nativa sin JNI
35. MemorySegment, MemoryLayout
36. Linker para llamar funciones nativas
37. JExtract para generar bindings
38. Java y AI/ML: DJL (Deep Java Library)
39. Java y AI: Tribuo para machine learning
40. Java y WebAssembly: TeaVM, JWebAssembly
41. Java en Cloud Native
42. Java en Serverless (AWS Lambda)
43. Java en Edge Computing
44. Java en IoT
45. Kotlin como complemento a Java
46. Kotlin coroutines vs virtual threads
47. Kotlin y Spring Boot
48. Java vs Kotlin: cuándo usar cada uno
49. Java User Groups y comunidad
50. Resumen: el futuro de Java

---

## MÓDULO 50: ARQUITECTURA DE SOFTWARE Y PRÁCTICAS SENIOR

**Descripción:** El módulo final te prepara para el nivel senior: arquitectura de sistemas, decisiones técnicas, liderazgo técnico, y la visión global que distingue a un senior developer.

1. ¿Qué hace un Senior Developer?
2. Leadership técnico sin ser manager
3. Code review: cómo hacerlo efectivamente
4. Architecture Decision Records (ADRs)
5. Technical debt: identificar y priorizar
6. Refactoring strategies
7. Clean Architecture aplicada
8. Domain-Driven Design aplicado
9. Event-driven architecture
10. Microservices vs Modular Monolith
11. Cuándo NO usar microservicios
12. API design best practices
13. Backward compatibility
14. API versioning strategies
15. Database design patterns
16. Caching strategies (multi-level)
17. Message queue design
18. Idempotency en APIs
19. Distributed transactions (Saga pattern)
20. CAP theorem en la práctica
21. Performance engineering
22. Profiling con JFR y JMC
23. Load testing con k6, Gatling
24. Chaos engineering (concepto)
25. Security by design
26. Threat modeling
27. DevOps culture
28. CI/CD pipeline design
29. Feature flags
30. Observability: logs, metrics, traces
31. SRE principles
32. SLIs, SLOs, SLAs
33. On-call y incident management
34. Documentation as code
35. ADRs, runbooks, design docs
36. RFC process para decisiones técnicas
37. Mentoring junior developers
38. Estimating software projects
39. Agile/Scrum/Kanban en la práctica
40. Cross-team collaboration
41. Tech stack evaluation
42. Build vs buy decisions
43. Open source contribution
44. System design interviews
45. Design a URL shortener
46. Design a chat system
47. Design a notification system
48. Design a rate limiter
49. Career growth: IC track vs Management track
50. Resumen: checklist final del desarrollador Java Senior

---

**Notas finales:**

- Cada módulo está diseñado para tomarse entre **2 y 4 semanas** de estudio con práctica.
- Los 50 módulos representan un camino de **aproximadamente 2 a 3 años** de estudio constante.
- **No avances sin practicar** cada tema con código real.
- Crea un repositorio en GitHub donde subas tus ejercicios.
- Cada tema debería incluir al menos **un ejercicio práctico** que escribas y ejecutes.
- **IntelliJ IDEA** es el IDE recomendado para Java; invierte tiempo en aprenderlo bien.
- Aprende **Spring Boot** bien: es el framework dominante en el ecosistema Java empresarial.
