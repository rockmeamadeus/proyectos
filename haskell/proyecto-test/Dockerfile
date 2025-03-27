# Usar la imagen oficial de Haskell con Stack y GHC 9.6.6
FROM haskell:9.6.6

# Actualizar e instalar herramientas necesarias
RUN apt-get update && apt-get install -y git curl

# Instalar GHC, Cabal y Stack en las versiones requeridas
RUN curl -sSL https://get-ghcup.haskell.org | sh -s -- --version=0.1.50.1
ENV PATH="/root/.ghcup/bin:$PATH"

# Instalar versiones específicas
RUN ghcup install ghc 9.6.6 && ghcup set ghc 9.6.6
RUN ghcup install cabal 3.12.1.0 && ghcup set cabal 3.12.1.0
RUN ghcup install stack 3.3.1 && ghcup set stack 3.3.1
RUN ghcup install hls 2.9.0.1 && ghcup set hls 2.9.0.1

# Crear carpeta de trabajo
WORKDIR /app

# Copiar los archivos del proyecto al contenedor
COPY . /app

# Instalar dependencias del proyecto
RUN stack config set system-ghc --global true && stack build --only-dependencies

# Construir el proyecto
RUN stack build

# Comando por defecto para ejecutar tests
CMD ["stack", "test"]
