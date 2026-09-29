# Estado da análise

Atualizado em 29/09/2026. Escopo desta etapa: identificar componentes suspeitos e registrar o que as evidências permitem afirmar. Nenhum arquivo do jogo deve ser executado no Windows normal.

## Amostra principal

| Campo | Valor observado |
| --- | --- |
| Nome reportado | `Bleach vs. Naruto.exe` |
| SHA-256 | `4281AA82E909EE9825436397897371788A10955AE53A0449140017B22CF8FE93` |
| Tamanho | 3.232.256 bytes (aprox. 3,08 MiB) |
| Arquitetura | PE 32-bit |

## Evidências observadas

### Microsoft Defender

- `Trojan:Win32/Conteban.A!ml` foi registrado para cópias do executável e colocado em quarentena.
- `Trojan:Win32/Wacatac.H!ml` foi registrado em uma cópia de análise em 28/09/2026 e colocada em quarentena. O evento consultado não permite afirmar, sozinho, se aquela instância chegou a executar.
- Arquivos compactados antigos também tiveram detecções (`Trojan:Win32/Suschil!rfn` e `Ravartar!rfn`). Os hashes e o membro exato responsável por cada alerta não estão disponíveis nesta documentação.

### VirusTotal

A página vinculada registra **46/69 mecanismos** sinalizando o executável. Essa proporção não deve ser interpretada como chance de infecção. O relatório de comportamento mostra os rótulos `enigma`, `obfuscated` e `detect-debug-environment`, além de classificações comportamentais relacionadas a descoberta de processos/sistema, evasão de sandbox e injeção de processo. Rótulos de comportamento são evidências para investigar, não uma confirmação de que cada técnica ocorreu com sucesso.

O relatório também mostra um processo filho em `%TEMP%` chamado `D40BVNU30DKUP3BW.exe`. Ele pode ser um stub desempacotado ou outro componente; ainda não há artefato bruto que confirme sua função. As resoluções DNS visíveis incluem `a1672.dscr.akamai.net` e `eip-terr-na.cdp1.digicert.com.akahost.net`; os dados disponíveis não identificam um servidor de comando e controle.

### Análise estática local

- O relatório PE registra 6 de 8 seções com entropia alta e apenas 8 imports visíveis, incluindo `LoadLibraryA`, `GetProcAddress` e `ShellExecuteA`. Isso é compatível com empacotamento e limita o que a tabela de imports revela.
- Os relatórios locais atribuem o empacotamento a Enigma Protector, mas `die-scan.txt` está vazio. A identificação do packer precisa ser repetida e preservada com a saída original da ferramenta.
- O relatório de depuração menciona detecção de depurador e o rótulo `USBLEN26`, mas não há trace bruto de execução anexado. Esses itens permanecem alegações do relatório, não comportamento reproduzido.

## Evidência reportada, ainda não confirmada

Hermes relatou propagação por USB. O ambiente, a mídia envolvida e os artefatos originais dessa observação não foram localizados; portanto, não há confirmação de cópia para um pendrive real.

## Execução dinâmica

Foi preparada uma configuração do Windows Sandbox com rede e clipboard desativados, executável montado em leitura e uma pasta isolada para saída. Em 29/09/2026, o usuário informou ter iniciado `TermService` e a configuração offline foi aberta novamente. **Até a última checagem, nenhum relatório havia sido coletado e a execução dentro do convidado não estava confirmada.** Não desative o Defender nem conecte mídia USB para tentar reproduzir a alegação.

Mesmo quando houver resultado, uma execução sem rede não prova ausência de comportamento condicionado à conectividade. Não tratar silêncio, travamento ou falta de detecção como evidência de limpeza.

## Conclusão provisória

O executável deve ser tratado como malicioso e mantido fora do Windows normal. As detecções conflitantes (`Conteban`, `Wacatac` e os rótulos do VirusTotal) não bastam para nomear com segurança uma única família nem para afirmar quais arquivos da extração são payloads. A próxima evidência útil é um relatório dinâmico bruto, correlacionado por hash, com árvore de processos, arquivos criados, alterações de registro e tentativas de rede dentro do Sandbox.
