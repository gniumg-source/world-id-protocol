Resumen
La versión v4.0 de World ID introduce la abstracción de cuentas en su núcleo, transformando un World ID de un único secreto a un registro abstracto en un registro público (llamado WorldIDRegistry) con múltiples claves autorizadas. Este cambio fundamental permite varias mejoras clave:

Compatibilidad con múltiples claves : los usuarios pueden generar pruebas utilizando múltiples autenticadores válidos (por ejemplo, en múltiples dispositivos, múltiples plataformas o múltiples aplicaciones) mientras mantienen la misma identidad.
Resistencia de protocolo mejorada : la compatibilidad con múltiples claves reduce la probabilidad de pérdida de todas las claves, la rotación y revocación de claves se admiten de forma nativa, y el usuario puede (opcionalmente) definir un agente de recuperación de identificación mundial (por ejemplo, como autenticación biométrica).
Proveedor de autenticador basado en web : un proveedor de autenticador web de referencia simplifica el uso de World ID directamente en los navegadores, lo que mejora la experiencia del usuario y el potencial de adopción.
Privacidad mejorada : el protocolo exige el uso único de anuladores para acciones a largo plazo, lo que evita el seguimiento y mantiene la integridad de la prueba.
Estos cambios, en conjunto, aumentan la seguridad, la privacidad y la usabilidad, a la vez que permiten aplicaciones más sofisticadas de verificación humana en la era de la IA. Para más detalles sobre los cambios técnicos, consulte el Resumen: ¿Qué está cambiando ?

Especificaciones del producto
A grandes rasgos, esta versión del Protocolo trata sobre la Abstracción de Cuentas . Un ID de Mundo ya no está vinculado a un único secreto, sino que es un registro abstracto creado públicamente WorldIDRegistrycon un conjunto definido de claves autorizadas que permiten al usuario interactuar con su ID de Mundo (un modelo mental similar es cómo las claves de acceso autorizan cuentas para sitios web específicos o cómo funcionan las billeteras de contratos inteligentes en el ecosistema Ethereum).

Gracias a la habilitación de otros autenticadores, se publicará un autenticador de referencia de código abierto basado en la web que reducirá parte de la sobrecarga del uso de un ID Mundial y simplificará la experiencia del usuario. Esta experiencia de usuario mejorada facilitará y extenderá la adopción del Protocolo.

Definiciones
Autenticador : Un agente de software o hardware (p. ej., una aplicación, un dispositivo, un cliente web o un servicio) que controla un conjunto de pares de claves autorizados para una cuenta de World ID y es funcionalmente capaz de interactuar con el protocolo, por lo que puede actuar en nombre de dicha cuenta. Un autenticador es el agente de los usuarios/titulares. Cada autenticador se registra en la cuenta WorldIDRegistrymediante sus pares de claves autorizados.
Nodos OPRF : Los nodos OPRF son un conjunto multipartito (MPC) de nodos responsables de permitir la generación de anuladores que los usuarios presentan a los RP para demostrar la unicidad.
Agente de Recuperación : Una entidad designada por el usuario con permiso especial para recuperar su Cuenta de World ID en caso de pérdida de todos los Autenticadores. Esta entidad puede ser un conjunto de entidades representadas con reglas abstractas (por ejemplo, mediante un contrato inteligente). Esta designación es opcional y se realiza en cadena.
Acción : Mantiene la definición de la versión anterior del Protocolo.
Anulador : Mantiene la definición de la versión anterior del Protocolo. Un anulador es un identificador de un solo uso que garantiza que una acción solo se pueda realizar una vez. Es similar a un ticket de un solo uso: el usuario genera un anulador mediante una prueba y lo presenta a un RP. Un anulador siempre será el mismo para el mismo usuario y el mismo RP+Acción.
Prueba de Unicidad : Una declaración donde un usuario demuestra que realiza una acción una sola vez y posee una credencial específica (por ejemplo, soy una persona única con una credencial PoH que vota en esta propuesta una sola vez ). Estas pruebas no pueden asociarse criptográficamente con ninguna otra prueba (por ejemplo, no entre RP, ni siquiera con el mismo RP).
Pruebas de Sesión : Se utilizan después de una Prueba de Unicidad inicial (donde sessionIdse genera un [nombre de usuario]) y posteriormente son proporcionadas por un RP para recibir una declaración que garantiza criptográficamente que se usa el mismo ID de Mundo (p. ej., tengo una cuenta con un RP y quiero demostrar que ahora tengo una nueva Credencial ). Estas pruebas no se pueden asociar entre RP, entre sesiones con el mismo RP ni con ninguna otra prueba.
Funcionalidad clave del producto
Aquí se indican las nuevas características o funcionalidades clave para esta versión de World ID (v4.0):

Compatibilidad con múltiples claves: Un ID de mundo no está vinculado a una sola clave. Un usuario puede generar pruebas en múltiples autenticadores válidos (p. ej., dispositivos o plataformas). Con la importante excepción de las propiedades de seguridad del autenticador, una prueba demuestra lo mismo a un RP, independientemente del autenticador utilizado.
Un usuario puede agregar o eliminar diferentes autenticadores válidos para administrar su ID mundial (Portabilidad).
Motivación: Permitir múltiples autenticadores contribuye a la descentralización del protocolo, sin depender de un único actor (como un único proveedor de autenticadores, p. ej., World App). Además, abstraer un ID de World en un registro conceptual, en lugar de un único secreto, permite la existencia segura y práctica de múltiples autenticadores, así como la recuperación en caso de pérdida y la rotación en caso de vulneración.
Recuperación: recupera el acceso al mismo ID mundial a través de agentes de recuperación.
Motivación: La recuperación es un componente fundamental de un protocolo de prueba de identidad humana (consulte el informe técnico para saber por qué). Si bien esperamos que los proveedores de autenticadores ofrezcan mecanismos de respaldo robustos, el usuario debe poder recuperar su ID de mundo y el estado relacionado en un escenario de contingencia.
Proveedor de autenticador web: Un autenticador limitado que permite el uso de World ID en el navegador web. Sirve como referencia para un autenticador y también para mejorar la experiencia de usuario (UX) en ciertos flujos de RP. La funcionalidad es limitada, ya que el registro de credenciales no está incluido en esta versión inicial.
Motivación : Un autenticador liviano basado en la web permite un uso más simple de World ID, lo que brinda una mejor experiencia de usuario y permitirá un mayor crecimiento ya que interactuar con los RP será significativamente más simple.
RP de confianza. Un autenticador puede identificar que una solicitud proviene de un RP válido.
Motivación: Los autenticadores deben poder identificar que generan pruebas para el destinatario correcto a fin de reducir la posibilidad de phishing de pruebas (por ejemplo, que un actor malicioso solicite una prueba dirigida a un RP diferente para saber si usted realizó esa acción). Además, esto permite la futura introducción de tarifas de protocolo.
Requisitos no funcionales
Privacidad.
Suponiendo que no haya colusión entre los nodos de cada sistema multipartito, la privacidad del usuario no puede verse comprometida por ninguna de las partes, ni por la correlación de múltiples acciones ni por la identificación directa de un usuario. Por ejemplo, es imposible saber que un usuario específico realizó una acción específica (identificación) o que el mismo usuario realizó dos acciones diferentes (correlación).
Al abordar el vector de ataque de colusión de un umbral (o todos) de nodos, que en el caso de los nodos OPRF podría potencialmente permitir la desanonimización de la actividad pasada, se cumple lo siguiente:
Escalar a un número muy grande de nodos (por ejemplo, n = 50-100) es técnica y pragmáticamente factible.
Se debe establecer una gestión rigurosa de claves (por ejemplo, HSM que impidan la extracción de claves y la destrucción de claves rotadas fuera de uso) de manera auditable.
Se introducen requisitos estrictos para los identificadores que proporciona el Protocolo. Consulte los detalles en las especificaciones técnicas.
No se permiten supercookies humanas. El estado permanente o enlazable preserva al máximo la privacidad y se rige por el protocolo. En este contexto, preservar la privacidad significa que no es posible identificar a una sola persona, ni siquiera con un seudónimo, durante un largo periodo sin su consentimiento. Cualquier identificación permanente o permanente expuesta debe protegerse como secreto.
Seguridad.
Una identificación mundial no es un secreto único que deba compartirse o que no pueda rotarse
No se puede recuperar una ID mundial ni agregar un autenticador sin una intención verificable del usuario (a través del conocimiento de una clave secreta de un autenticador autorizado).
La colusión de todos los nodos con un sistema multipartidista (MPC) no permite realizar acciones en nombre del usuario.
Auditabilidad del usuario: cada usuario debe poder ver los eventos de administración de cuentas que se han autorizado con su ID mundial, por ejemplo, cosas como agregar o eliminar autenticadores.
Ruta de migración.
Debe haber una ruta de migración clara para todos los casos de uso actualmente activos y relevantes para la nueva versión del Protocolo
Flujos de usuario (Autenticador)
Wireframes ilustrativos de una experiencia de autenticador.

Otras consideraciones
Se han mejorado las implicaciones de privacidad y seguridad de los autenticadores (revocación de claves, etc.), pero el usuario debe confiar en su(s) autenticador(es). El autenticador debe gestionar correctamente las credenciales del usuario (o, anteriormente, los paquetes de custodia personal) y las claves
Especificaciones técnicas
Consejo

Tenga en cuenta que estas son las especificaciones técnicas de alto nivel en el momento de la introducción de World ID 4.0. La documentación técnica más actualizada que refleja el estado actual del Protocolo siempre se puede encontrar en la documentación para desarrolladores y en el repositorio del Protocolo

Resumen: ¿Qué está cambiando?
Una ID mundial ahora es un registro en un registro en cadena y, lo que es más importante, una única ID mundial puede tener múltiples claves públicas.
Esto también significa que los compromisos de identidad ( identityCommitment) ya no existen. En su lugar, el mecanismo de identificación es el conocimiento de una clave secreta correspondiente a una clave pública registrada en un índice de hoja específico en el WorldIDRegistry.
También implica que los árboles en cadena de compromisos de identidad han desaparecido en favor de uno solo WorldIDRegistry.
La creación de un ID de Mundo ahora se realiza mediante el registro en cadena (en lugar de la generación de un par de claves sin conexión, como antes), y la emisión de Credenciales se realiza sin interacción en cadena. Las credenciales ahora son emitidas por el Emisor que las firma. Anteriormente, el Emisor añadía el compromiso de identidad del usuario al árbol en cadena correspondiente.
Los anuladores son de un solo uso. Anteriormente, no se exigía que los anuladores fueran de un solo uso y podían convertirse en identificadores seudónimos para un RP. Ahora, los autenticadores no emitirán un anulador más de una vez.
[ Solo para RPs ]. Cuando los RPs requieren que los usuarios demuestren que siguen siendo el mismo ID de Mundo que realizó originalmente una acción, podrán almacenar un identificador de la acción original (a sessionId) y proporcionárselo al usuario para comprobaciones posteriores. Con la Prueba de Humanidad, los RPs pueden demostrar que interactúan con el mismo ID de Mundo, aunque posiblemente también con credenciales diferentes. Consulte Pruebas de Sesión para más detalles.
[ Solo para emisores ]. La autenticación basada en el uso de anuladores de ZKP como identificadores ya no es compatible. Se introduce un nuevo mecanismo de autenticación para emisores.
Se puede recuperar el acceso a una ID de Mundo. Un usuario puede designar un Agente de Recuperación para su cuenta, lo que permitirá la recuperación en caso de perder el acceso a todos los Autenticadores.
[ Alcance del Agente de Recuperación ] Los usuarios pueden designar el sistema PoH AMPC como su Agente de Recuperación para recuperar su ID de Mundo. Se espera que otros Agentes de Recuperación estén disponibles en el futuro.
Descripción general de alto nivel
Diagrama de componentes para el Protocolo World ID 4.0. Diagrama de componentes del Protocolo World ID 4.0.

Se presenta el Registro World ID . Este contrato público es la fuente de la verdad para los World ID; un World ID se convierte conceptualmente en una cuenta, representada en una hoja del árbol de Merkle en este contrato. Cada cuenta se identifica con su índice en el árbol. El registro también contiene una lista de claves públicas de autenticador autorizadas para actuar en nombre del titular. Los nodos OPRF, así como los RP, utilizan esto para verificar las pruebas (a través de una prueba de inclusión de Merkle dentro de los ZKP).

De igual forma, se introduce un Registro de Partes Confiables . Este registro contiene una lista de Partes Confiables autorizadas con sus correspondientes claves públicas autorizadas. El registro permite a los RP autenticar las solicitudes de pruebas a los Autenticadores.

Se introduce el conjunto multipartito de nodos OPRF . Este conjunto de nodos se encarga de generar los anuladores que los usuarios presentan a los RP para demostrar la unicidad. Los anuladores se generan mediante una Función Pseudoaleatoria Olvidada del Umbral Verificado (vOPRF) con la participación de los nodos OPRF. Los nodos verifican que las solicitudes de anuladores sean validadas correctamente tanto por los RP como por los usuarios (véase Pruebas de Unicidad ), y solo entonces generarán la salida necesaria para calcular el anulador del usuario. Los usuarios construyen el anulador final y demuestran su cálculo en la prueba que presentan a los RP.

Una OPRF multipartita es necesaria porque evita que los anuladores sean adivinables; es decir, los anuladores son deterministas, pero parecen aleatorios (recuerde que las salidas de PRF bajo una clave uniformemente aleatoria son computacionalmente indistinguibles de una función uniformemente aleatoria). Esto podría lograrse teóricamente con una función hash regular, pero entonces los anuladores podrían ser sometidos a un ataque de fuerza bruta calculando el hash de todos los posibles leafIndexES (que son públicos en la cadena). Para evitar esto, se requiere entropía secreta (en un ID de mundo ≤ 3.0, el usuario proporcionó esta entropía). Dado que esto ya no está disponible, la entropía ahora proviene de los nodos OPRF.
Además, para evitar ataques de fuerza bruta, incluso con la participación de nodos OPRF, estos requieren autenticación antes de calcular cada hash. Autentican al usuario mediante un ZKP que demuestra el conocimiento de una clave secreta de autenticador autorizada para el caso WorldIDRegistryparticular leafIndexpara el que generan un anulador.
Es importante destacar que los nodos OPRF calculan la función hash con clave
H
k
(
x
′
)
en una entrada ciega, por lo tanto, no pueden saber qué usuario está realizando realmente una solicitud. Además, los nodos OPRF generan una prueba que da fe del cálculo correcto de
H
k
dado un compromiso
k
pág
k
, por lo que ni los usuarios ni los RP necesitan confiar ciegamente en los nodos OPRF
De manera similar a cómo se utilizan los nodos OPRF para generar los anuladores presentados a los RP, estos nodos también generan un factor cegador para cada credencial, de modo que no pueda haber correlación entre los identificadores mundiales y los emisores maliciosos.
Puede encontrarse más información sobre los nodos OPRF en el documento: “ Un protocolo anulador basado en un OPRF de umbral verificable ” .
Se deben establecer detalles sobre la naturaleza, el número y los requisitos de diversidad de los nodos OPRF antes de que la red de producción esté activa.
Diferencias de protocolo de un vistazo:

ID de mundo ≤3.0	ID de mundo 4.0 (2025)
¿Qué es un ID de mundo?	Un secreto	Una entrada en el registro público.
Generación de pruebas	Pruebas de semáforo generadas en el cliente.	Conceptualmente igual, pero con nuevos circuitos ZK. Los usuarios generan una prueba de consulta para los nodos OPRF, que proporcionan cálculos que permiten la generación del anulador. Se genera una prueba de unicidad final y se presenta a los RP
¿Cómo la parte confiada hace cumplir la unicidad?	Almacenar un hash anulador.	Conceptualmente lo mismo.
Privacidad posterior a la vulneración	Si se filtra el secreto de World ID del usuario, se podría identificar toda la actividad pasada.

Además, el secreto no se puede rotar	Si se filtra el secreto del autenticador de un usuario, no se puede identificar ninguna actividad pasada por sí sola. Se requeriría una connivencia con un RP para comprometer alguna actividad pasada.

Los secretos se pueden rotar fácilmente.
Recuperabilidad	No se puede recuperar si se pierde el secreto.	Se puede recuperar opcionalmente a través de un agente de recuperación
Emisión de credenciales	Árbol Merkle en cadena que contiene idComms.

Credencial equivalente mantenida bajo custodia propia.	Mensaje firmado por el emisor.

Credencial en custodia.
Señal (mensajes de prueba)	Un RP puede incluir una señal arbitraria a la que el usuario se compromete	Conceptualmente lo mismo.
Seguridad secreta	El secreto debe almacenarse con protecciones de software y cargarse en la memoria	Es conceptualmente posible almacenar claves en almacenes de claves basados ​​en hardware. Las claves iniciales tendrán las mismas características que la versión anterior del protocolo debido a las limitaciones de la prueba ZK.
Detalles técnicos
Pruebas de unicidad
Una prueba de unicidad es la forma en que un usuario demuestra principalmente que realiza una acción una sola vez y que posee una credencial que cumple con los requisitos del RP (por ejemplo, el usuario tiene un documento único emitido por el gobierno). Si bien fundamentalmente el usuario demuestra la unicidad por cuenta de World ID al realizar una acción, si la solicitud no está vinculada a una credencial que ofrezca una medida de unicidad (por ejemplo, PoH o un documento único emitido por el gobierno), la prueba carecerá de valor


El anulador es calculado por los nodos OPRF. Su cálculo requiere la salida de un número umbral de nodos para que sea válido

Es importante destacar que la entrada a los nodos OPRF está ciega, de modo que ningún nodo OPRF puede ver el contenido sin procesar leafIndex(es decir, los nodos OPRF solo saben que la solicitud proviene de un autenticador autorizado).
Es importante destacar que el anulador es independiente de las credenciales , por lo que la acción solo se puede realizar una vez, independientemente de qué credenciales estén disponibles en ese momento.
Puede encontrar más información sobre cómo se calcula el anulador en el documento técnico OPRF de TACEO .
Los anuladores tienen las siguientes propiedades, que en combinación los hacen aptos para que un RP los use para imponer la unicidad anónima por acción:

Propiedad	Descripción
Determinista	Dado el mismo contexto ( leafIndex[blinded], rpId, action), el anulador siempre es el mismo. Suponiendo un comportamiento honesto de los nodos OPRF que nunca rotan su clave base. Tenga en cuenta que la credencial no se incluye intencionalmente en este contexto. Esto significa que la acción solo se puede realizar una vez, independientemente de las credenciales que estén disponibles en ese momento
Indiscutible	Para un contexto fijo, la salida del anulador se distribuye uniformemente en el espacio de salida. Incluso con el conjunto completo de posibles usuarios, calcular anuladores candidatos es inviable sin la colusión de un umbral de nodos OPRF tal que se conozca la clave OPRF
Autenticado	Es probabilísticamente imposible reclamar la propiedad de un anulador si no se conoce un valor secreto (una clave secreta cuya contraparte pública está registrada en el WorldIDRegistry).
Anónimo	Un anulador oculta quién lo generó. Para preservar el anonimato, cada anulador solo debe usarse una vez (de lo contrario, su uso repetido lo convierte en un seudónimo). Esto es responsabilidad de los autenticadores.
No vinculable	Para dos anuladores cualesquiera con diferentes contextos, la probabilidad de que un adversario pueda distinguir correctamente si se derivaron del mismo usuario es, como mucho, insignificantemente mejor que la de una suposición aleatoria
Resistencia de preimagen	Para cualquier anulador dado, y conociendo el contexto público ( rpId, action), es computacionalmente inviable encontrar la preimagen o leafIndexla
El autenticador genera dos tipos de pruebas de conocimiento cero diferentes para poder entregar una prueba de unicidad a un RP,

La prueba de consulta
π
1
que demuestra a los nodos OPRF que la solicitud está correctamente autorizada por el usuario. Esta ZKP demuestra que la solicitud está firmada por una clave pública que está registrada para el usuario en particular, proporcionada leafIndexen WorldIDRegistryel
Una prueba final de unicidad
π
2
que garantiza al menos las siguientes restricciones:
Se evalúan las mismas restricciones de la prueba de consulta
Evaluación OPRF correcta en leafIndex, es decir, el anulador generado es correcto para las claves públicas comprometidas de cada nodo OPRF.
La solicitud se firma mediante una clave pública que está registrada en leafIndexla WorldIDRegistry(autenticación de usuario).
La credencial fue emitida para esta identificación mundial, es decir, la credencial subcoincide con el cegamiento leafIndexdel usuario.
La Credencial utilizada en la prueba está firmada por el Emisor (a través de la clave comprometida en el CredentialSchemaIssuerRegistry).
La credencial no está vencida.
La credencial cumple con la restricción mínima genesis_issued_at proporcionada por el RP.
La señal y el nonce proporcionados por el RP como entradas públicas están comprometidos.
Las posibles restricciones futuras pueden incluir: certificación de integridad del dispositivo, aplicación de la expiración de acciones, verificaciones específicas de credenciales, etc.
Grupo de Anuladores Inocentes . El Grupo de Anuladores Inocentes es un servicio independiente que ofrece la Recuperación de Intersecciones Privadas y realiza un seguimiento de los anuladores utilizados. Su función es simplemente mantener una lista plana de anuladores usados, de modo que un autenticador pueda consultar si se ha utilizado un anulador antes de compartirlo (y los datos relacionados).
π
2
) con un RP si se ha usado anteriormente. La lista es plana (ya que el anulador ya es único por RP, por acción y por usuario), basándose en la propiedad de resistencia a colisiones de la función hash utilizada en el Protocolo.

Este sistema garantiza que los anuladores no se puedan usar indebidamente para crear identificadores de larga duración. Como su nombre indica, un anulador es de un solo uso.
El término "olvidado" se utiliza para referirse al hecho de que este mapa se consulta de una manera en que los servidores que atienden dichas solicitudes no pueden saber a qué registros se accedió y, por lo tanto, pueden comprometer la privacidad del usuario.
La principal limitación del grupo de anuladores es el rendimiento a escala. Una opción es fragmentar el grupo, compensando el tamaño del conjunto de anonimato con el rendimiento. Esto aún se encuentra en fase de investigación.
Inicialmente, este grupo solo se usará para acciones con un período de ejecución superior a un umbral predefinido. Esto sirve para solucionar problemas de escalabilidad a medida que el sistema crece.
Sujetos cegados . Para evitar la correlación de usuarios, incluso entre emisores, o en caso de filtración de credenciales, se cega a los sujetos de las credenciales.

Al solicitar una nueva credencial a un emisor, el usuario genera un factor de cegamiento utilizando los nodos OPRF,
factor de cegamiento del sujeto
=
H
k
(
ID de esquema del emisor
∣∣
índice de hoja
)
.
El usuario luego combina el factor de cegamiento con su leafIndexpara calcular la subreclamación de la credencial. Este valor es el que los emisores incluyen en la credencial.
Cuando se presenta una prueba, subjectBlindingFactorse utiliza dentro del circuito de Prueba de Unicidad para garantizar que la credencial se emita al usuario correcto. El factor de cegamiento actúa como entropía para evitar la correlación, pero la información correcta leafIndexproporcionada en la entrada del circuito debe coincidir correctamente.
Registros
Registro de ID mundial
Cada usuario puede otorgar acceso a múltiples claves diferentes para interactuar con su ID mundial. El autenticador demuestra el control dentro de un ZKP para evitar identificadores de larga duración
Para evitar filtraciones del usuario, esto debe estar en una estructura que permita pruebas de inclusión. Esto se logra mediante árboles de Merkle incrementales .
Cada autenticador registra dos claves en el registro. Esto permite operaciones eficientes tanto en cadena como en circuitos de conocimiento cero.
Una clave en cadena, que es una clave de curva elíptica, secp256k1se utiliza para autorizar operaciones en cadena en el contrato (por ejemplo, añadir o eliminar un autenticador, etc.). La clave pública se representa simplemente como una dirección de Ethereum.
Una clave fuera de la cadena, que es una clave de curva elíptica en la BabyJubJubcurva, se utiliza para firmar solicitudes de pruebas de conocimiento cero. La clave pública (representada como un punto de curva) se emite en la cadena y se compromete en el contrato.
Registro de Parte Confiada
Cada RP debe comprometerse con su clave pública autorizada en el registro público, de modo que esto pueda verificarse en la prueba de solicitud
π
1
por cada nodo OPRF consultado.
Registrar un RP es una acción pública que cualquiera puede realizar, pero requiere el pago de una tarifa de registro única (consulte Tarifas de registro a continuación).
Para permitir la creación y el registro de aplicaciones descentralizadas, el Registro RP se ampliará y se eliminarán aún más restricciones en el futuro, pero para esta versión inicial se aplica lo siguiente:
En el lanzamiento, solo se permite una clave autorizada por RP. Esto se ampliará en el futuro.
Registro de emisores de esquemas de credenciales
Es un registro simple donde los emisores registran un esquema y un firmante autorizado para cada tipo de credencial, y obtienen un ID issuerSchemaId. Este ID representa la combinación de un (emisor, esquema). Por ejemplo: (Herramientas para la Humanidad, credencial Orb).
Se issuerSchemaIdincluye en la credencial y se verifica como parte de todas las pruebas. Al generar y verificar las pruebas, la firma de una credencial se verifica con la clave pública registrada en el contrato.
El registro de un Esquema de Emisor también requiere el pago de una tarifa de registro única (ver Tarifas de Registro a continuación).
Tarifas de registro
Tanto el Registro de Partes Confiables como el Registro de Emisores del Esquema de Credenciales cobran una tarifa de registro única. La infraestructura de tarifas sirve como un mecanismo de limitación de velocidad sin permisos (una alternativa a restringir el registro a las personas autorizadas que llaman), lo que garantiza que el registro permanezca abierto a cualquier persona y, al mismo tiempo, previene el abuso

¿Por qué existe la tarifa? El registro de un RP o un Esquema de Emisor activa la inicialización de una clave OPRF mediante una ceremonia de generación de claves distribuida en múltiples rondas entre los nodos OPRF. Esta operación requiere un alto coste computacional y de infraestructura. La tarifa de registro cubre el coste de la generación y el almacenamiento de la clave OPRF durante al menos un año aproximadamente.

Cómo funciona.

La tarifa se paga en un token ERC-20 configurable safeTransferFromen el momento del registro, antes de que comience la generación de la clave OPRF
Futuro: Tarifas por solicitud. La tarifa de registro descrita aquí cubre únicamente el costo único de la incorporación. Es posible que en una futura versión del Protocolo (4.1 o 4.2) se introduzca una tarifa por solicitud independiente, impuesta por los nodos OPRF como requisito de comprobante de pago durante la generación de anuladores. Consulte las Notas de Preparación para el Futuro para obtener más información.

Recuperación
La recuperación se introduce para el caso en que se pierde el acceso a todos los autenticadores (o sus claves). La recuperación permite a los usuarios recuperar el control de su ID de mundo registrando un nuevo autenticador y revocando los perdidos. Cada usuario puede designar un agente de recuperación con un rol especial para realizar la recoverAccountoperación. Este rol especial puede recuperar el ID de mundo de un usuario y nada más, y a la inversa, solo estos agentes pueden realizar una recoverAccountoperación

Importante

Esta sección define la recuperación como un protocolo primitivo. Cada agente de recuperación proporcionará su propio conjunto de especificaciones sobre cómo proporcionar la recuperación de ID de mundo

Diagrama conceptual del proceso de recuperación

Una recoverAccountoperación es una función definida en el WorldIDRegistrycontrato que recibe un mensaje firmado del Agente de Recuperación con una nueva clave pública de autenticador. La operación da como resultado el registro del nuevo autenticador y la revocación de todos los antiguos. El estado histórico de los autenticadores está disponible en la cadena.
El mensaje firmado es compatible con ERC-1271 , lo que significa que puede provenir de un contrato inteligente que establece sus propias reglas para la recuperación. Por ejemplo, un agente de recuperación puede requerir firmas de varias partes para permitir una recuperación. Además, esto permite definir un agente de recuperación como una entidad abstracta regida por su propio contrato inteligente.
Es importante destacar que la recuperación solo será posible para los usuarios del nuevo Protocolo. En esencia, no es posible recuperar los World IDs previamente perdidos, ya que se trata de un secreto perdido. Se están implementando alternativas para mitigar esto; consulte " Consideraciones de Migración" para obtener más información.
La designación de un agente de recuperación es completamente opcional y se puede actualizar en cualquier momento.
Una vez recuperada una cuenta de World ID, se pueden solicitar nuevas credenciales a cada emisor correspondiente. Cada emisor puede definir sus propias reglas para recuperar sus credenciales.
Consideración futura. En el futuro, se podría introducir una nueva función que permita usar un World ID como firmante en otra cosa. Por ejemplo, una firma de World ID podría usarse como factor para recuperar una billetera de criptomonedas. Si bien esta funcionalidad se basa en la primitiva de recuperación, es independiente de esta y no está dentro de su alcance.
Pruebas de sesión
Los RP pueden crear sesiones para su aplicación para garantizar que siga siendo el mismo ID de mundo el que interactúa con ellos en múltiples interacciones. Las pruebas de sesión permiten intencionalmente que el RP vincule múltiples interacciones en su aplicación con el mismo ID de mundo. Los posibles casos de uso incluyen:

Actualización de credenciales: Un usuario se verificó previamente con una credencial y ahora desea probarla con otra (por ejemplo, para desbloquear recompensas adicionales). RP debe asegurarse de que la nueva credencial pertenezca al mismo titular.
Verificación de vencimiento de credenciales: un usuario previamente registrado con una credencial; en cada inicio de sesión consecutivo, el RP desea asegurarse de que la credencial del usuario aún sea válida (por ejemplo, que no esté vencida).
(Futuro). Autenticación facial a nivel de RP: Actualmente, la autenticación facial solo garantiza que quien presente la prueba sea la misma persona que recibió la credencial. Sin embargo, en algunas aplicaciones, también es necesario garantizar que, durante múltiples interacciones, un RP pueda verificar que siempre fue la misma persona.
Las pruebas de sesión utilizan los mismos circuitos de conocimiento cero que las pruebas de unicidad, pero los autenticadores deben distinguirlas claramente para los usuarios, ya que implican un identificador reutilizable que puede vincular interacciones. Las pruebas de sesión se limitan al nivel de RP y no requieren ninguna acción de este. En lugar de un anulador, las pruebas de sesión devuelven un, sessionNullifierque es necesario para la verificación, pero no ofrece la misma garantía de unicidad.

Las pruebas de sesión funcionan de la siguiente manera:

Un RP inicia una solicitud de prueba.
La prueba genera un sessionId. Un identificador único vinculado al ID mundial del usuario para ese RP.
El RP almacena esto sessionIdjunto con la información de su cuenta para el usuario.
Para interacciones posteriores, el RP incluye las sessionIdsolicitudes de prueba. El usuario puede generar una prueba de sesión para demostrar que comparten el mismo ID de mundo.
El sessionIdse genera como se describe a continuación, donde res un número distribuido uniformemente derivado de rpId.

Proveedor de autenticador basado en web
Para permitir una mejor experiencia de usuario, se está introduciendo un proveedor de autenticador de referencia basado en navegador. Esta aplicación proporciona la funcionalidad de World ID (actualmente limitada), pero sin salir del navegador

A grandes rasgos, permite el uso de un World ID. El usuario puede generar pruebas en su navegador, lo cual resulta especialmente útil al trabajar en otros dispositivos (como computadoras de escritorio) o con aplicaciones no nativas.
Cuando un RP requiere la prueba de World ID de un usuario, puede simplemente redirigirlo a la aplicación web (gestionada automáticamente por SDK comunes como ID Kit ). El usuario se autentica con su clave de acceso, genera la prueba en su navegador y la envía al RP.
Se publicará documentación adicional sobre la arquitectura del proveedor de autenticador de referencia basado en web en el repositorio https://github.com/worldcoin/web-authenticator .
La inscripción de credenciales no será compatible con la versión inicial, pero es posible que se incorpore en el futuro.
Consideraciones de migración
A grandes rasgos, todos los usuarios y RP deberán migrar al nuevo protocolo. Las rutas de migración detalladas se publicarán en la documentación para desarrolladores

Consideraciones de privacidad
El protocolo, a través del grupo de anuladores Oblivious, exige que los anuladores no se puedan generar más de una vez (siempre que los autenticadores se implementen correctamente), lo que evita el seguimiento prolongado de usuarios, lo que aumenta la privacidad con respecto a la versión anterior del protocolo

En escenarios adversarios, estas son las consideraciones de privacidad más relevantes,

Escenario de ataque	ID de mundo ≤3.0	ID de mundo 4.0 (2025)
Secreto del usuario comprometido	⚠️ Potencialmente revela toda la actividad pasada si el atacante conoce los ID y las acciones de las aplicaciones públicas	✅ No puede revelar actividad pasada por sí solo
RP malicioso	✅ Un RP malicioso por sí solo no revela actividad pasada	✅ Un RP malicioso por sí solo no revela actividad pasada
Nodo OPRF malicioso	N/D	✅ No se puede comprometer la actividad pasada del usuario
Colusión de nodos OPRF de umbral+	N/D	⚠️ Podría revelar la actividad pasada del usuario (pero requiere tener anuladores para comparar, por ejemplo, a través de colusión RP)
Secreto de usuario comprometido + colusión de RP	⚠️ Potencialmente revela toda la actividad pasada. Ataque sin conexión.	⚠️ Puede revelar la actividad pasada del usuario para ese RP. Ataque en línea (requiere llamadas a nodos OPRF).
Autenticador malicioso	⚠️ Potencialmente revela toda la actividad pasada si el atacante conoce los ID y las acciones de las aplicaciones públicas	⚠️Un autenticador malicioso o comprometido podría revelar la actividad del usuario. Esto probablemente podría llevar a que los usuarios depositen su confianza en los autenticadores de código abierto.
Coerción del usuario	⚠️ Potencialmente revela toda la actividad pasada. Ataque sin conexión.	⚠️ Puede forzar la revelación de anuladores no vencidos que, en combinación con RP u otra información, pueden revelar actividad pasada.
Otras consideraciones de riesgo
Los nodos OPRF funcionan con un m-of-numbral. Si
n
−
m
+
1
Si los nodos pierden sus claves, se perderá el estado del protocolo, no habrá forma de generar los anuladores correctos y se perderá el estado de las acciones «consumidas» o realizadas
Censura por parte de nodos OPRF. Estos nodos podrían rechazar la generación de anuladores para los usuarios. Es difícil que esto sea un ataque dirigido debido a su leafIndexcegamiento, pero podrían censurar RP o acciones específicas.
Riesgo del autenticador. Además de tener acceso a las credenciales del usuario, un autenticador debe conocer sus datos sin leafIndexprocesar para generar pruebas. Un autenticador malicioso puede usar esto indebidamente para rastrear al usuario, aunque dicho rastreo no pueda correlacionarse con los anuladores proporcionados a los RP. Se están explorando diferentes estrategias para mitigar el riesgo del autenticador.
Riesgo del Agente de Recuperación. Si un usuario designa un Agente de Recuperación, esta entidad cuenta con un permiso especial que le permite acceder a su ID de Mundo, lo que conlleva sus propios riesgos. Los usuarios deben considerar los diferentes riesgos asociados a los distintos Agentes de Recuperación, ya que no todos son iguales.
[Alcance del Emisor]. En el caso específico de la credencial Orb & PoH AMPC, los usuarios que opten por no recuperar la biometría y pierdan todas sus claves de autenticación no podrán obtener una nueva credencial PoH por el momento. Esto podría cambiar en el futuro a discreción de los Emisores.
Notas de preparación para el futuro (futuras versiones de World ID 4.x y posteriores)
Esta no es una lista exhaustiva, pero describe temas generales que pueden ser el objetivo de próximos lanzamientos del Protocolo y que actualmente no están cubiertos en este lanzamiento.

Autorización facial. La firma del emisor en la credencial permitirá la introducción de una verificación de autenticación facial demostrable (con la confianza del sensor de la cámara) durante la generación de la prueba.
Políticas y conjunto de permisos del autenticador. En esta versión, WorldIDRegistrysolo contiene una lista plana de claves públicas, pero podría actualizarse para convertirla en una estructura de datos más compleja que codifique permisos explícitos para cada clave, de modo que cada autenticador pueda tener una política diferente para cada acción (por ejemplo, agregar un autenticador o generar una prueba), lo cual puede verificarse públicamente.
Pruebas del lado del cliente. Con la introducción de las pruebas del lado del cliente y, posteriormente, otros tipos de pruebas (por ejemplo, la certificación de edad), será posible combinar las pruebas de unicidad con certificaciones adicionales.
Emisores que tienen la capacidad de revocar credenciales.
Establecer confianza entre las partes del protocolo (por ejemplo, identificar un autenticador confiable).
Capacidad de fusionar múltiples ID mundiales, lo que se traduce en la capacidad de rotar identificadores con cada emisor.
En el registro de RP. En el futuro, la confianza de RP también podría basarse en otros mecanismos existentes, como su nombre de dominio (DNS). Además, las acciones podrían registrarse públicamente para su auditabilidad y cumplimiento.
Identificación mundial como firmante (o recuperación biométrica). De forma similar a cómo es posible recuperar una identificación mundial gracias a que PoH AMPC permite añadir un nuevo autenticador, será conceptualmente posible que una identificación mundial pueda ser un firmante de recuperación para otras cuentas.
Protección contra phishing a prueba de intermediarios (MITM). Si bien el vector de ataque de phishing a prueba se ha reducido con la introducción del registro RP, aún es posible realizar pruebas MITM. Se requieren mecanismos de protección adicionales para mitigar esto.
En el futuro, las credenciales podrían ser específicas del autenticador, y los emisores podrían firmarlas para su uso únicamente con un autenticador específico.
Es posible que en el futuro se introduzcan tarifas por solicitud (enfocándose en las versiones 4.1 o 4.2) de modo que los nodos OPRF reciban un comprobante de pago como parte de la solicitud para generar un anulador. Esto es distinto de la tarifa de registro única ya vigente (véase Tarifas de Registro ).
Admite operaciones criptográficas que permiten que los secretos puedan residir en hardware seguro y no exportarse nunca.
