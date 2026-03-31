#PROMPT
{language code: R; role: R programmer; Task:create a script to connect to Google Drive using R studio, Product:script explained that connect to my google drive folder and have acess to create, read, delete, and edit folders and files; Rules:
    1.   Login
        usuario
        senha
        api google cloud
    
    2.   Caminho da pasta
    
      [https://drive.google.com/drive/folders/1sQRcEJzjav0g677g5X7CEG1OHTX0E3Ba?hl=en ](https://drive.google.com/drive/my-drive )
      
      https://drive.google.com/drive/folders/1sQRcEJzjav0g677g5X7CEG1OHTX0E3Ba?usp=sharing
    
    3.   Chamada da pasta
    
        Script deve acessar pasta com privilegio de editor, e esse acesso deve ser permanente. 
    
    4.   Acessar o Crud 
        leitura
        Criar
        Editar
        Deletar
    
    5. Requisitos
      minha pasta pessoal
      script em r
      acesso completo como editor)}

#EXEMPLO DE CÓDIGO!!!!

install.packages("remotes")
remotes::install_github("danicat/read.dbc")
library(read.dbc)


############################################
# GOOGLE DRIVE - CARREGAR TODOS OS ARQUIVOS
############################################

# 1) INSTALAÇÃO E CARREGAMENTO
if (!require("googledrive")) install.packages("googledrive")
library(googledrive)

# 2) AUTENTICAÇÃO
drive_auth(scopes = "https://www.googleapis.com/auth/drive",
           cache = ".secrets", use_oob = TRUE)

# 3) PASTA DE TRABALHO
PASTA_ID <- "1sQRcEJzjav0g677g5X7CEG1OHTX0E3Ba"
pasta_trabalho <- drive_get(as_id(PASTA_ID))
cat("Pasta:", pasta_trabalho$name, "\n")

# 4) LISTAR E BAIXAR TODOS OS ARQUIVOS
arquivos <- drive_ls(as_id(PASTA_ID))

for (i in 1:nrow(arquivos)) {
  cat("Baixando:", arquivos$name[i], "\n")
  drive_download(as_id(arquivos$id[i]),
                 path = arquivos$name[i],
                 overwrite = TRUE)
}

# 5) LISTAR ARQUIVOS BAIXADOS
cat("\n--- Arquivos carregados no ambiente ---\n")
list.files()

cat("\n--- Pronto! Todos os arquivos estão na pasta de trabalho ---")
