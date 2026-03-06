Contratos del Protocolo de Identificación Mundial
Todos los contratos del Protocolo de Identificación Mundial están diseñados explícitamente para operar detrás de un contrato proxy para permitir actualizaciones. Hay algunas consideraciones importantes de implementación:

Las actualizaciones de cualquier contrato se realizan creando un nuevo contrato con un V{number}sufijo que hereda de la versión anterior (p. ej., WorldIDRegistryV2.sol). Esto mantiene un control de versiones explícito para las actualizaciones del contrato y facilita la comprensión de los cambios en cada versión. También ayuda a prevenir clases de almacenamiento accidentales.
Un ejemplo de esto se puede encontrar en la versión anterior del Protocolo de Identificación Mundial (3.0).
Todas las funciones con acceso menos restringido de lo privatedebido se marcarán virtualpara permitir la corrección de errores en la interfaz existente. Esto permite anularlas en futuras actualizaciones.
Generalmente, todas las variables/miembros deben estar marcados internal, y las variables que deberían ser públicas deben exponer un método getter anotado con el símbolo " onlyProxyy" onlyInitialized. Esto garantiza que las variables solo se lean desde el proxy, evitando posibles problemas.
Todas las variables/funciones miembro que tienen menos restricciones de acceso que las que privatese deben marcar internalpara que se pueda acceder a ellas en nuevas versiones de los contratos.
Cualquier función que lea o modifique el estado (es decir, que no esté marcada como pure) debe anotarse con los modificadores onlyProxy``` y ` onlyInitialized`. Esto garantiza que solo se pueda llamar cuando tenga acceso a los datos del proxy; de lo contrario, los resultados podrían ser incoherentes.
Asegúrese de que toda la funcionalidad recién agregada tenga un acceso cuidadosamente controlado mediante onlyOwner, o un mecanismo de acceso más granular según corresponda.
No asigne ninguna variable a nivel de contrato en el sitio de definición a menos que sean constant.
La inicialización y la gestión de la propiedad no están protegidas onlyProxyintencionalmente. Esto garantiza que el contrato pueda eliminarse de forma segura una vez que ya no se utilice.
