# Waheed Oladunjoye: portfolio site

Static site served by Nginx in a small Docker image.

## Run locally
    docker compose up -d --build
    open http://localhost

## Deploy on AWS EC2 (free tier)
1. Launch an Amazon Linux 2023 or Ubuntu instance. In the security group, allow inbound TCP 80 and 443 (anyone) and 22 (your IP only).
2. Install Docker and the Compose plugin:
   - Amazon Linux: `sudo dnf install -y docker && sudo systemctl enable --now docker`, then install the compose plugin (see Docker docs).
   - Ubuntu: follow https://docs.docker.com/engine/install/ubuntu/
3. Copy this folder to the instance: `scp -r waheed-site ec2-user@<public-ip>:~/`
4. On the instance: `cd waheed-site && sudo docker compose up -d --build`
5. Visit `http://<public-ip>`.

## Update the site
Edit files in `site/`, then run `sudo docker compose up -d --build`.

## Notes
- `site/assets/Waheed_Oladunjoye_CV.pdf` is the downloadable CV. It contains a phone number; replace it with a version without one if you prefer.
- For HTTPS on your own domain, point the domain's A record to the instance's Elastic IP and put Caddy or an AWS load balancer in front.
