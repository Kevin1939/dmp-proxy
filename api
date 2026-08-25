// Vercel Serverless Function - 反向代理
export default async function handler(req, res) {
    const path = req.url || '/';
    const targetUrl = "http://175.178.175.105/dmp-prd" + path;

    try {
        const response = await fetch(targetUrl, {
            headers: {
                'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36'
            }
        });
        const content = await response.text();
        let contentType = 'text/html; charset=utf-8';
        if (path.endsWith('.js')) contentType = 'application/javascript; charset=utf-8';
        else if (path.endsWith('.css')) contentType = 'text/css; charset=utf-8';
        else if (path.endsWith('.png')) contentType = 'image/png';
        else if (path.endsWith('.jpg') || path.endsWith('.jpeg')) contentType = 'image/jpeg';

        res.setHeader('Content-Type', contentType);
        res.status(200).send(content);
    } catch (error) {
        res.status(500).send('代理请求失败：' + error.message);
    }
}
