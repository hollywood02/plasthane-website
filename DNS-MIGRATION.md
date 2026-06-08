# Migration DNS — plasthane.com vers Vercel

## Contexte

Le nouveau site est hébergé sur **Vercel**. Il faut modifier les enregistrements DNS chez **Vidéotron** (nameservers actuels) pour que `plasthane.com` pointe vers Vercel au lieu de l'ancien hébergement (67.205.73.116).

## Informations du domaine

- **Domaine :** plasthane.com
- **Registrar :** Tucows Domains Inc. (via HostPapa)
- **Fournisseur DNS actuel :** Vidéotron (`dns1.videotron.net` / `dns2.videotron.net`)
- **Gestion technique :** Bifusion (bifusion.com)
- **Expiration :** 2026-12-31

## Configuration Vercel

- `plasthane.com` → redirige 307 vers `www.plasthane.com`
- `www.plasthane.com` → Production

## Enregistrements DNS à configurer

| Type | Nom | Ancienne valeur | Nouvelle valeur |
|------|-----|-----------------|-----------------|
| **A** | `@` | `67.205.73.116` | `216.198.79.1` |
| **CNAME** | `www` | `plasthane.com` | `bd51d8acfdb33ab6.vercel-dns-0f7.com` |

### Important

- **Supprimer** les anciens enregistrements A et CNAME qui pointent vers l'ancien hébergement
- **Ne PAS toucher** aux enregistrements MX (courriels)
- Les nameservers Vidéotron restent en place — on change seulement les records A et CNAME

## Étapes

1. Se connecter au panneau DNS chez Vidéotron (accès via Bifusion)
2. Supprimer l'ancien enregistrement A pour `@` (67.205.73.116)
3. Supprimer l'ancien enregistrement CNAME pour `www`
4. Ajouter le nouvel enregistrement A : `@` → `216.198.79.1`
5. Ajouter le nouvel enregistrement CNAME : `www` → `bd51d8acfdb33ab6.vercel-dns-0f7.com`
6. Attendre la propagation DNS (5 min à 48h, généralement < 1h)
7. Aller sur Vercel → Settings → Domains → cliquer **Refresh** sur les deux domaines
8. Vercel va automatiquement générer le certificat SSL

## Vérification après migration

- [ ] `plasthane.com` redirige vers `www.plasthane.com`
- [ ] `www.plasthane.com` charge le nouveau site
- [ ] Le cadenas HTTPS est présent
- [ ] Les courriels @plasthane.com fonctionnent toujours
- [ ] Les deux domaines dans Vercel affichent "Valid Configuration"

## URL de preview (en attendant la migration)

`plasthane-website.vercel.app`
