# hqr
二维码


## 示例

```
package main

// dev2
import (
	"github.com/honsty/hqr"

	"net/http"
)

func main() {
	http.HandleFunc("/qr", Qr)

	http.ListenAndServe(":8080", nil)
}

func Qr(w http.ResponseWriter, r *http.Request) {
	r.ParseForm()
	text := r.URL.Query().Get("text")

	code, err := hqr.Encode(text, hqr.H)
	if err != nil {
		w.Write([]byte("Server Error."))
		return
	}
	w.Header().Set("Content-Type", "image/png")
	w.Write(code.PNG())
}

```