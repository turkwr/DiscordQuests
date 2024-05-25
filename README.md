# Discord görevlerini tamamlayın!
Discord üzerinde "Bir Görev" tamamlandı rozetine sahip olmak için aşağıdaki adımları takip edin. Böylece rozete sahip olabileceksiniz.
![image](https://github.com/turkwr/DiscordQuests/assets/63150613/59f2be0e-6de9-4c08-b885-3401d2834b80)
> Bu kod web üzerinden çalışmamaktadır.

## Adım 1: Görevi aktif edin.
![image](https://github.com/turkwr/DiscordQuests/assets/63150613/5a0c1b2e-5b68-48ed-845b-c2bd21bc87f0)
**Ayarlar > Hediye Envanteri** sayfasına girdiğiniz zaman bulunan görevi kabul edin, bu rozeti alacağınız zamana göre değişiklik gösterebilir.
## Adım 2: DevTools'u aktif edin.
Discord masaüstü uygulamasında `Ctrl` + `Shift` + `I` tuşlarına tıklayın.
* Herhangi bir şey olmuyor mu? O zaman buradan devam edin!
  1. `Windows` + `R` ile "Çalıştır"'ı başlatın.
  2. `%appdata%` yazın.
  3. `discord` klasörünü bulun. Eğer Discord Canary kullanıyorsanız `discordcanary` yazacaktır. Buna dikkat edin. ![image](https://github.com/turkwr/DiscordQuests/assets/63150613/a1238750-03ef-4d15-aad4-b359988ed6d8)
  4. `settings.json` dosyasını bulun. Bunu herhangi bir editörle açın. (Not Defteri veya herhangi bir kod editörü.) ![image](https://github.com/turkwr/DiscordQuests/assets/63150613/86e79f43-be77-4660-b9fc-33cd80ff7eeb)
  5. Açtıktan sonra `"DANGEROUS_ENABLE_DEVTOOLS_ONLY_ENABLE_IF_YOU_KNOW_WHAT_YOURE_DOING": true,` yazısını tam olarak bu şekilde yazmanız gerekmektedir. Herhangi bir yanlışlık veya virgül hatası yapmayın. Aksi takdirde bir şeyleri bozabilirsiniz. ![image](https://github.com/turkwr/DiscordQuests/assets/63150613/0cd2e2c5-8d9c-4e08-b9f1-67eac1d09f75)



## Adım 3: Bir arkadaşınızı çağırın.
Rozeti alabilmek için bir arkadaşınızın ekranınızı izlemesi gerekmektedir. Bu yüzden arkadaşınızla sesli bir odaya girin.
## Adım 4: Tam ekran paylaşın.
Ekranızı tam bir şekilde açın ve arkadaşınızdan ekranı izlemesini isteyin.
## Adım 5: Kodu yapıştırın.
`Ctrl` + `Shift` + `I` yaptıktan sonra yukarıdan `Console` sekmesine giriyoruz.
Bu konsol kısmına verdiğim kodu yapıştıracaksınız.
> Kodu yapıştıramıyorsanız ilk önce __BU YAZIYI KOPYALAMADAN__ `allow pasting` yazmanız gerekmektedir.
> ![image](https://github.com/turkwr/DiscordQuests/assets/63150613/3495edbe-ee90-446f-ad6b-1bed2be77d00)
```js
let wpRequire;
window.webpackChunkdiscord_app.push([[ Math.random() ], {}, (req) => { wpRequire = req; }]);

let ApplicationStreamingStore = Object.values(wpRequire.c).find(x => x?.exports?.default?.getStreamerActiveStreamMetadata).exports.default;
let QuestsStore = Object.values(wpRequire.c).find(x => x?.exports?.default?.getQuest).exports.default;
let FluxDispatcher = Object.values(wpRequire.c).find(x => x?.exports?.default?.flushWaitQueue).exports.default;

let quest = [...QuestsStore.quests.values()].find(x => x.userStatus?.enrolledAt && !x.userStatus?.completedAt && new Date(x.config.expiresAt).getTime() > Date.now())
let isApp = navigator.userAgent.includes("Electron/")
if(!isApp) {
	console.log("Lütfen masaüstü uygulamasında çalıştırın.")
} else if(!quest) {
	console.log("Herhangi tamamlanmamış bir göreve sahip değilsin!")
} else {
	let pid = Math.floor(Math.random() * 30000) + 1000
	ApplicationStreamingStore.getStreamerActiveStreamMetadata = () => ({
		id: quest.config.applicationId,
		pid,
		sourceName: null
	})
	
	let secondsNeeded = quest.config.streamDurationRequirementMinutes * 60
	let fn = data => {
		let progress = data.userStatus.streamProgressSeconds
		console.log(`Görev ilerlemesi: ${progress}/${secondsNeeded}`)
		
		if(progress >= secondsNeeded) {
			console.log("Görev tamamlandı!")
			FluxDispatcher.unsubscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
		}
	}
	FluxDispatcher.subscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
	
	console.log(`Akışınızı ${quest.config.applicationName}'e spamladı. sesli odada ${Math.ceil(quest.config.streamDurationRequirementMinutes - (quest.userStatus?.streamProgressSeconds ?? 0) / 60)} dakika daha kalın.`)
	console.log("Sesli odada en az 1 kişiye daha ihtiyacınız olduğunu unutmayın!")
}
```
## Adım 6: Sesten çıkmadan bekleyin.
**Ayarlar > Hediye Envanteri** sayfasını sürekli kontrol ederek adımların ilerleyip ilerlemediğini kontrol edin. Eğer 1-2 dakikadır devam etmiyorsa kodu tekrar yapıştırın.
## Adım 7: Rozeti alın.
15 dakika geçtikten sonra **Ayarlar > Hediye Envanteri** sayfasından "Ödülü Al" butonuna tıklayın.

Tebrikler 🎉! Artık **"Bir Görev Tamamlandı"** rozetine sahipsin!

- Herhangi bir sorun olmasında Discord üzerinden benimle iletişime geçebilirsiniz.
- [@turkwr - 162740870607536128](https://discord.com/users/162740870607536128)

## Ayrıca:
Kod bana ait değildir, sadece orijinal hali Türkçe'ye çevrilmiştir. Eğer kodda bir hata alırsanız orijinal halini kontrol edin.
[Orijinal haline erişmek için tıkla.](https://gist.github.com/aamiaa/204cd9d42013ded9faf646fae7f89fbb)
