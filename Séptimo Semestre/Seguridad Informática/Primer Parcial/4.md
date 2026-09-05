## Model for Network Security

ISOs are based on a framework (ISO 27001 ISMS) designed to protect information.
```
ISO 27001 ISMS → Security services {Mecanisms}
	↓                                 ↓
Certification               Confidentiality→
			                Data integrity→
			                Non repudiation→   Criptography
			                Authentication →         ↓
			                                    Hash Functions
```

Los algoritmos de cripto pueden dividirse en encriptación simétrica (shaded Key AB which keeps on third party) o asimétrica (public and private keys KA+, KA-, KB+, KB-).

El algoritmo de encriptación toma el texto y lo cifra utilizando la key. Posteriormente se utiliza un algoritmo para desencriptar la información.

```
     A ------------------- B
     ↓                     ↓
C=E(M, KAB)            M=D(C, KAB)
```

Con esto se logra confidencialidad, pero no integridad; para ello se requiere de hash codes. Igual se provee autenticación (gracias a las keys). Para lograr non repudiation también se requieren hash functions.

Asúmase que se tiene el mensaje `M` original (1000bits posibles). Para reducir el tamaño de los datos, se pasa el mensaje por un HC, obteniendo de ello `H(M)` (signature), que pesa 160 bits. `M`+`H(M)`. 

Para lograr cubrir los 4 servicios, se aplica:

$$
C=E(M+HM, K_{AB})
$$

1. Design a suitable algorithm for the security transformation.
2. Generated the secret keys used by the algorithm.
3. Develop methods to distribute and share the secret information.
4. Specify a protocol enabling the principals to use the transformation and secret information for a security service.

Todo esto es para simétrica.

Para asimétrica:

```

 E(K_B}^+)               
	 A -------------------- B
	 ↓                      ↓
K_{A}^+,K_{A}^-	      K_{B}^+,K_{B}^-
     ↓                      ↓
C=E(K_^+, M)          C=E(K_^+, M)
       
```

Estas claves pueden generarse mediante: *prime numbers* (en la simétrica solo son enteros), que deben ser sumamente grandes (como $79191827746573111111$). Al venir ambas claves de un mismo número primo,

Compartir la clave pública puede provocar DNS spoofing; para lo que usamos https (443) (que implementa SSL/TLS (dentro tienen crypto algorithms)). Http (80) es altamente interceptable. HTTPS brinda un certificado, que es lo que previene el spoofing. Se usa un certificado para cada end del servicio $C_A$, $C_B$, que serán emitidos por un third party de confianza (no son session keys). El algoritmo es RSA (last names).

Posterior al access channel, se requiere tener una gatekeeper function. 

1. Select appropiate gatekeeper functions to identify users (password based login procedures, IDS/IPS, FIrewalls, ACL)
2. Implement security controls that monitors activity to ensure only authorized users access designated information or resources.

## Methods of Defense

1. Data encryption
2. Software control (monitor and gatekeeping)
3. Hardware control
4. Policies
5. Use biometrics (science of identifying or verifyng a person based on psysiological or behavioral characteristics).

### Biometrics:

- Biometrics (science of identifying or verifyng a person based on psysiological or behavioral characteristics).
- Authentication: Validating or figuring out the identity of a person → P,K,B
- Authorization: Permission or approval.

There are 3 ways of verifiying (PKB):
- Possessions
- Knowledge
	- Secrets
	- Non secrets
- Biometrics
	- Physiological
	- Behavioral

These are sometimes combined (e.g. ATM machines)

Disconnected token (current time + account info + algorithm → hash code)

## Five Steps to Better Security

- Assets: What is to be protected (consider where we are)
	- E-commerce: Addresses, credit card numbers, etc
- Risks: What are the threat vectors, vulnetabilities and risks?
	- A threat vector describes what a threat is and where it comes from
- Protection: How will the assets be protected
	- Security mecanisms and policies
- Tools: What will be done to ensure that protection
	- Product evaluation to implement security policies
- Priorities: In what order will the protective steps will be implemented.

## Building a Secure Organization

Security is not about hardware and software. That is, no product or combination of products will create a secure organization by itself. Security is a process.

Steps to this:

- Evaluate the Risks and Threats
- Provide Security Training for IT Staff
- Think out of the box
- Develop a culture of security
- Identify and utilize built in security features (update OS)
- Hire a third party
- Dont forget the basics
- PATCH PATCH PATCH