<script lang="ts">

export const validURL = (url: string): boolean => {
    var pattern = new RegExp('^(https?:\\/\\/)?'+ // protocol
        '((([a-z\\d]([a-z\\d-]*[a-z\\d])*)\\.)+[a-z]{2,}|'+ // domain name
        '((\\d{1,3}\\.){3}\\d{1,3}))'+ // OR ip (v4) address
        '(\\:\\d+)?(\\/[-a-z\\d%_.~+]*)*'+ // port and path
        '(\\?[;&a-z\\d%_.~+=-]*)?'+ // query string
        '(\\#[-a-z\\d_]*)?$','i'); // fragment locator
    return !!pattern.test(url);
}

export const deepCopy = <T>(object: T): T => {
    return JSON.parse(JSON.stringify(object))
}

type OS = 'Mac OS'|'iOS'|'Windows'|'Android'|'Linux'|''

export const getOS = (): OS => {
    const userAgent = window.navigator.userAgent
    // @ts-ignore
    const platform = window.navigator?.userAgentData?.platform || window.navigator.platform
    const macosPlatforms = ['Macintosh', 'MacIntel', 'MacPPC', 'Mac68K', 'macOS']
    const windowsPlatforms = ['Win32', 'Win64', 'Windows', 'WinCE']
    const iosPlatforms = ['iPhone', 'iPad', 'iPod']
    let os: OS = ''

    if (macosPlatforms.indexOf(platform) !== -1) {
        os = 'Mac OS';
    } else if (iosPlatforms.indexOf(platform) !== -1) {
        os = 'iOS';
    } else if (windowsPlatforms.indexOf(platform) !== -1) {
        os = 'Windows';
    } else if (/Android/.test(userAgent)) {
        os = 'Android';
    } else if (/Linux/.test(platform)) {
        os = 'Linux';
    }

    return os
}

export const socketEmitter = async (socket: any|undefined, event: string, data?: any) => {
    return await new Promise((resolve, reject) => {
        if (!socket) return reject('Socket not connected')

        socket.emit(event, data, (response: any) => {
            if (response && response.error) reject(response.error)
            else resolve(response)
        })
    })
}

export const socketHandler = async (socket: any|undefined, event: string, callback?: (res: any)=>void) => {
    if (!socket) return

    socket.on(event, callback)
}

export default {
    validURL,
    deepCopy,
    getOS,
    socketEmitter,
    socketHandler
}

</script>
