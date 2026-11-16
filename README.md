# Lista IPTV Brasil

Playlist M3U de TV ao vivo do Brasil, gerada e atualizada automaticamente para uso no Nuvio (ou em qualquer player que aceite M3U).

## Como usar

Copie a URL abaixo e cole no player, na opção de lista por URL:

```
https://raw.githubusercontent.com/PeixotoSilvastm/iptv-brasil-peixoto/main/playlist.m3u8
```

## O que tem na lista

Só canais do Brasil, organizados em quatro grupos:

- **Esportes**
- **Notícias**
- **Filmes**
- **Abertas** (TV aberta nacional e alguns canais regionais)

## Como funciona

1. O workflow `.github/workflows/update.yml` roda a cada 6 horas (e pode ser disparado manualmente na aba **Actions**).
2. Ele baixa o catálogo de canais e o estado de cada um (vivo ou fora do ar) do repositório [Nuvio-KE-channels](https://github.com/Arshad-Kamal/Nuvio-KE-channels).
3. Mantém só os canais que estão funcionando, remove duplicatas e grava o `playlist.m3u8`.
4. Se algo for alterado, o commit é feito automaticamente. Se nada mudou, nada é gravado.

### Proteções

- Se o download das fontes falhar, ou se a lista sair pequena demais, a playlist anterior é mantida.
- Se o monitor do repositório de origem ficar mais de 3 dias sem atualização, o workflow falha de propósito para avisar que a lista pode estar desatualizada.
- URLs que exigem cabeçalhos especiais (Referer, User-Agent) são ignoradas.
- Fontes por endereço IP direto só entram se estiverem estáveis ao longo do dia.

## Ajustes

As configurações ficam no começo do script dentro do `update.yml`:

| Opção | O que faz |
| --- | --- |
| `MAX_PER_CHANNEL` | Quantas URLs por canal (a melhor + reservas) |
| `KEEP_GROUPS` | Quais grupos entram na lista |
| `STALE_DAYS` | Dias sem atualização do monitor até o alerta |
| `MIN_SLOTS_IP_HOST` | Estabilidade mínima exigida de fontes por IP |

## Observações

- Canais de TV ao vivo na internet podem sair do ar a qualquer momento. A lista se corrige sozinha nas próximas atualizações.
- A lista não hospeda nenhum conteúdo. Ela só reúne links de transmissões que já estão públicos.

## Créditos

- [Arshad-Kamal/Nuvio-KE-channels](https://github.com/Arshad-Kamal/Nuvio-KE-channels): catálogo e monitoramento dos canais.
- [iptv-org/iptv](https://github.com/iptv-org/iptv): base de dados de canais usada pelo catálogo acima.
