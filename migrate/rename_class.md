# Renomeando as classes

Ao migrar para o PHP 8 e Codeigniter 3, o primeiro passo é renomear todos os arquivos de classes, garantindo que a primeira letra seja maiúscula. Por exemplo, se o projeto contém o módulo home/controllers/home.php, ele deve ser renomeado para home/controllers/Home.php.

Aqui está um pequeno trecho de código em PHP que pode facilitar essa tarefa:

```
$diretorioPrincipal = FCPATH . 'application/modules/';

        if (is_dir($diretorioPrincipal)) {
            if ($dh = opendir($diretorioPrincipal)) {
                // Loop através das pastas principais
                while (($pastaPrincipal = readdir($dh)) !== false) {
                    if ($pastaPrincipal != '.' && $pastaPrincipal != '..') {
                        $caminhoPastaPrincipal = $diretorioPrincipal . $pastaPrincipal;

                        // Verifica se é um diretório
                        if (is_dir($caminhoPastaPrincipal)) {
                            // Loop através das subpastas "controllers" e "modules"
                            foreach (['controllers', 'models'] as $subpasta) {
                                $caminhoSubpasta = $caminhoPastaPrincipal . '/' . $subpasta;

                                if (is_dir($caminhoSubpasta)) {
                                    if ($dhSubpasta = opendir($caminhoSubpasta)) {
                                        // Loop através dos arquivos na subpasta
                                        while (($nomeArquivo = readdir($dhSubpasta)) !== false) {
                                            if ($nomeArquivo != '.' && $nomeArquivo != '..') {
                                                $caminhoCompletoAntigo = $caminhoSubpasta . '/' . $nomeArquivo;
                                                $caminhoCompletoNovo = $caminhoSubpasta . '/' . ucfirst($nomeArquivo);

                                                // Renomeia o arquivo
                                                if (rename($caminhoCompletoAntigo, $caminhoCompletoNovo)) {
                                                    echo "Nome do arquivo modificado: $caminhoCompletoAntigo -> $caminhoCompletoNovo\n";
                                                } else {
                                                    echo "Erro ao renomear o arquivo: $caminhoCompletoAntigo\n";
                                                }
                                            }
                                        }
                                        closedir($dhSubpasta);
                                    }
                                }
                            }
                        }
                    }
                }
                closedir($dh);
            }
        } else {
            echo "O diretório principal especificado não existe.\n";
        }
```

> **ALERTA:** Lembre-se de executar isso com cuidado, fazendo backup dos arquivos antes de realizar as mudanças.
