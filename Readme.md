# mathlibdanval — utilidades matemáticas básicas en Python

Pequeña librería con funciones matemáticas frecuentes, pensada como ejemplo de empaquetado, pruebas y CI en Python. Incluye operaciones como **`square`**, **`factorial`**, **`is_prime`**, **`gcd`** y **`lcm`**. El repo ya está organizado como paquete (`src/`), con pruebas en `tests/` y flujos de GitHub Actions para CI y releases. ([GitHub][1])

## 🚀 Instalación

**Opción A — desde el repositorio (recomendada si estás iterando):**

```bash
pip install -U pip
pip install git+https://github.com/Danval-003/mathlib.git
```

**Opción B — editable (desarrollo local):**

```bash
git clone https://github.com/Danval-003/mathlib.git
cd mathlib
python -m venv .venv
# Windows
.\.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -U pip
pip install -e .
```

> Si más adelante publicás a PyPI, también podrás instalar con `pip install mathlibdanval` (ajusta el nombre al que figure en tu `pyproject.toml`).

## 🧭 Uso rápido

```python
from mathlibdanval import square, factorial, is_prime, gcd, lcm

print(square(3))      # 9
print(factorial(5))   # 120
print(is_prime(97))   # True
print(gcd(48, 18))    # 6
print(lcm(7, 3))      # 21
```

### Errores y casos borde

Las funciones validan tipos y condiciones de entrada:

* `factorial(n)` lanza `ValueError` si `n < 0` y `TypeError` si no es `int`.
* `is_prime(n)` lanza `ValueError` si `n < 0` y `TypeError` si no es `int`.
* `gcd(a,b)` y `lcm(a,b)` lanzan `ValueError` si `a == b == 0` y `TypeError` si no son enteros.
* `lcm` devuelve siempre un resultado **no negativo**.

## 🧪 Pruebas

El repo incluye pruebas unitarias con **pytest** que cubren caminos felices, bordes y errores.

```bash
pip install -r requirements-dev.txt  # si existe
pip install pytest                   # si no tenés dev deps
pytest -q
```

> En cada Pull Request y en cada push, GitHub Actions corre automáticamente los tests en una matriz de versiones de Python. Si algo falla, el PR/push marca rojo y no avanza el release. (Tu repo ya tiene `src/`, `tests/` y workflows en `.github/workflows/`.) ([GitHub][1])

## 🔁 CI/CD y releases

* **CI (PR/Push):** ejecuta `pytest` y sube reporte JUnit como artefacto.
* **Release:** usa `python-semantic-release` + `build` + `twine`. Al taguear según convención (o al ejecutar el paso de versionado), se construye la distribución y, si configuraste los secretos, se sube a PyPI.

> Asegurate de definir en *Settings → Secrets and variables → Actions* los tokens necesarios (por ejemplo, `PYPI_API_TOKEN`) si vas a publicar.

## 📂 Estructura

```
.
├─ src/
│  └─ mathlibdanval/        # paquete (implementación)
├─ tests/                   # pruebas unitarias (pytest)
├─ .github/workflows/       # CI y release
├─ pyproject.toml           # metadatos de paquete
└─ README.md
```

[1]: https://github.com/Danval-003/mathlib "GitHub - Danval-003/mathlib"
