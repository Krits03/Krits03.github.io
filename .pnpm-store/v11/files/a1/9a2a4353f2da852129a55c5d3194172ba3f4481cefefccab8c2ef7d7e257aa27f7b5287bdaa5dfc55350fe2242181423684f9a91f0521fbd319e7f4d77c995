const e = new TextDecoder(), t = (t, n = 0, r = t.length) => e.decode(t.slice(n, r)), n = (e, t = 0, n = e.length) => e.slice(t, n).reduce((e, t) => e + (`0` + t.toString(16)).slice(-2), ``), r = (e, t = 0) => {
	let n = e[t] + e[t + 1] * 2 ** 8;
	return n | (n & 2 ** 15) * 131070;
}, i = (e, t = 0) => e[t] * 2 ** 8 + e[t + 1], a = (e, t = 0) => e[t] + e[t + 1] * 2 ** 8, o = (e, t = 0) => e[t] + e[t + 1] * 2 ** 8 + e[t + 2] * 2 ** 16, s = (e, t = 0) => e[t] + e[t + 1] * 2 ** 8 + e[t + 2] * 2 ** 16 + (e[t + 3] << 24), c = (e, t = 0) => e[t] * 2 ** 24 + e[t + 1] * 2 ** 16 + e[t + 2] * 2 ** 8 + e[t + 3], l = (e, t = 0) => e[t] + e[t + 1] * 2 ** 8 + e[t + 2] * 2 ** 16 + e[t + 3] * 2 ** 24, u = {
	readUInt16BE: i,
	readUInt16LE: a,
	readUInt32BE: c,
	readUInt32LE: l
};
function d(e, t, n, r) {
	n ||= 0;
	let i = r ? `BE` : `LE`, a = `readUInt` + t + i;
	return u[a](e, n);
}
const ee = {
	validate: (e) => t(e, 0, 2) === `BM`,
	calculate: (e) => ({
		height: Math.abs(s(e, 22)),
		width: l(e, 18)
	})
};
function f(e, t) {
	let n = e[t];
	return n === 0 ? 256 : n;
}
function p(e, t) {
	let n = 6 + t * 16;
	return {
		height: f(e, n + 1),
		width: f(e, n)
	};
}
const m = {
	validate(e) {
		let t = a(e, 0), n = a(e, 4);
		return t !== 0 || n === 0 ? !1 : a(e, 2) === 1;
	},
	calculate(e) {
		let t = a(e, 4), n = p(e, 0);
		if (t === 1) return n;
		let r = [n];
		for (let n = 1; n < t; n += 1) r.push(p(e, n));
		return {
			height: n.height,
			images: r,
			width: n.width
		};
	}
}, te = {
	validate(e) {
		let t = a(e, 0), n = a(e, 4);
		return t !== 0 || n === 0 ? !1 : a(e, 2) === 2;
	},
	calculate: (e) => m.calculate(e)
}, h = {
	validate: (e) => l(e, 0) === 542327876,
	calculate: (e) => ({
		height: l(e, 12),
		width: l(e, 16)
	})
}, g = /^GIF8[79]a/, _ = {
	validate: (e) => g.test(t(e, 0, 6)),
	calculate: (e) => ({
		height: a(e, 8),
		width: a(e, 6)
	})
}, v = {
	validate: (e) => {
		let n = y(e, `ftyp`);
		if (!n) return !1;
		let r = t(e, n.offset + 8, n.offset + 12);
		return [
			`heic`,
			`heix`,
			`hevc`,
			`hevx`,
			`mif1`,
			`msf1`
		].includes(r);
	},
	calculate: (e) => {
		let t = y(e, `meta`);
		if (!t) throw TypeError(`heic: meta box not found`);
		let n = y(e, `iprp`, t.offset + 12, t.offset + t.size);
		if (!n) throw TypeError(`heic: iprp box not found`);
		let r = y(e, `ipco`, n.offset + 8, n.offset + n.size);
		if (!r) throw TypeError(`heic: ipco box not found`);
		let i = b(e, `ispe`, r.offset + 8, r.offset + r.size).map((t) => ({
			width: c(e, t.offset + 12),
			height: c(e, t.offset + 16)
		}));
		if (i.length === 0) throw TypeError(`heic: ispe box not found`);
		let a = i[0];
		for (let e = 1; e < i.length; e++) {
			let t = i[e];
			t.width * t.height > a.width * a.height && (a = t);
		}
		return a;
	}
};
function y(e, n, r = 0, i = e.length) {
	let a = r;
	for (; a < i;) {
		let r = c(e, a);
		if (t(e, a + 4, a + 8) === n) return {
			offset: a,
			size: r
		};
		if (r <= 0 || a + r > i) break;
		a += r;
	}
}
function b(e, n, r = 0, i = e.length) {
	let a = r, o = [];
	for (; a < i;) {
		let r = c(e, a);
		if (t(e, a + 4, a + 8) === n && o.push({
			offset: a,
			size: r
		}), r <= 0 || a + r > i) break;
		a += r;
	}
	return o;
}
const x = {
	ICON: 32,
	"ICN#": 32,
	"icm#": 16,
	icm4: 16,
	icm8: 16,
	"ics#": 16,
	ics4: 16,
	ics8: 16,
	is32: 16,
	s8mk: 16,
	icp4: 16,
	icl4: 32,
	icl8: 32,
	il32: 32,
	l8mk: 32,
	icp5: 32,
	ic11: 32,
	ich4: 48,
	ich8: 48,
	ih32: 48,
	h8mk: 48,
	icp6: 64,
	ic12: 32,
	it32: 128,
	t8mk: 128,
	ic07: 128,
	ic08: 256,
	ic13: 256,
	ic09: 512,
	ic14: 512,
	ic10: 1024
};
function S(e, n) {
	let r = n + 4;
	return [t(e, n, r), c(e, r)];
}
function C(e) {
	let t = x[e];
	return {
		width: t,
		height: t,
		type: e
	};
}
const ne = {
	validate: (e) => t(e, 0, 4) === `icns`,
	calculate(e) {
		let t = e.length, n = c(e, 4), r = 8, i = S(e, r), a = C(i[0]);
		if (r += i[1], r === n) return a;
		let o = {
			height: a.height,
			images: [a],
			width: a.width
		};
		for (; r < n && r < t;) i = S(e, r), a = C(i[0]), r += i[1], o.images.push(a);
		return o;
	}
}, re = {
	validate: (e) => n(e, 0, 4) === `ff4fff51`,
	calculate: (e) => ({
		height: c(e, 12),
		width: c(e, 8)
	})
}, w = {
	ftyp: `66747970`,
	jp2h: `6a703268`,
	jp__: `6a502020`,
	rreq: `72726571`
}, ie = (e) => {
	let t = e[0], n = 1 + 2 * t, r = i(e, n) * (2 + t);
	n = n + 2 + r;
	let a = i(e, n) * (16 + t);
	return n + 2 + a;
}, T = (e) => ({
	height: c(e, 4),
	width: c(e, 8)
}), E = {
	validate(e) {
		let t = n(e, 4, 8), r = c(e, 0);
		if (t !== w.jp__ || r < 1) return !1;
		let i = r + 4, a = c(e, r), o = e.slice(i, i + a);
		return n(o, 0, 4) === w.ftyp;
	},
	calculate(e) {
		let r = c(e, 0), a = i(e, r + 2), o = r + 4 + a;
		switch (n(e, o, o + 4)) {
			case w.rreq: return o = o + 4 + 4 + ie(e.slice(o + 4)), T(e.slice(o + 8, o + 24));
			case w.jp2h: return T(e.slice(o + 8, o + 24));
			default: throw TypeError(`Unsupported header found: ` + t(e, o, o + 4));
		}
	}
};
function D(e) {
	return n(e, 2, 6) === `45786966`;
}
function O(e, t) {
	return {
		height: i(e, t),
		width: i(e, t + 2)
	};
}
function k(e, t) {
	let n = d(e, 16, 14, t);
	for (let r = 0; r < n; r++) {
		let n = 16 + r * 12, i = n + 12;
		if (n > e.length) return;
		let a = e.slice(n, i);
		if (d(a, 16, 0, t) === 274) return d(a, 16, 2, t) !== 3 || d(a, 32, 4, t) !== 1 ? void 0 : d(a, 16, 8, t);
	}
}
function A(e, t) {
	let r = e.slice(2, t), i = n(r, 6, 8), a = i === `4d4d`;
	if (a || i === `4949`) return k(r, a);
}
function j(e, t) {
	if (t > e.length) throw TypeError(`Corrupt JPG, exceeded buffer limits`);
	if (e[t] !== 255) throw TypeError(`Invalid JPG, marker table corrupted`);
}
const M = {
	validate: (e) => n(e, 0, 2) === `ffd8`,
	calculate(e) {
		e = e.slice(4);
		let t, n;
		for (; e.length > 0;) {
			let r = i(e, 0);
			if (D(e) && (t = A(e, r)), j(e, r), n = e[r + 1], n === 192 || n === 193 || n === 194) {
				let n = O(e, r + 5);
				return t ? {
					height: n.height,
					orientation: t,
					width: n.width
				} : n;
			}
			e = e.slice(r + 2);
		}
		throw TypeError(`Invalid JPG, no size found`);
	}
}, N = {
	validate: (e) => t(e, 1, 7) === `KTX 11`,
	calculate: (e) => ({
		height: l(e, 40),
		width: l(e, 36)
	})
}, P = `CgBI`, F = {
	validate(e) {
		if (t(e, 1, 8) === `PNG\r

`) {
			let n = t(e, 12, 16);
			if (n === P && (n = t(e, 28, 32)), n !== `IHDR`) throw TypeError(`Invalid PNG`);
			return !0;
		}
		return !1;
	},
	calculate(e) {
		return t(e, 12, 16) === P ? {
			height: c(e, 36),
			width: c(e, 32)
		} : {
			height: c(e, 20),
			width: c(e, 16)
		};
	}
}, I = {
	P1: `pbm/ascii`,
	P2: `pgm/ascii`,
	P3: `ppm/ascii`,
	P4: `pbm`,
	P5: `pgm`,
	P6: `ppm`,
	P7: `pam`,
	PF: `pfm`
}, L = {
	default: (e) => {
		let t = [];
		for (; e.length > 0;) {
			let n = e.shift();
			if (n[0] !== `#`) {
				t = n.split(` `);
				break;
			}
		}
		if (t.length === 2) return {
			height: Number.parseInt(t[1], 10),
			width: Number.parseInt(t[0], 10)
		};
		throw TypeError(`Invalid PNM`);
	},
	pam: (e) => {
		let t = {};
		for (; e.length > 0;) {
			let n = e.shift();
			if (n.length > 16 || (n.codePointAt(0) || 0) > 128) continue;
			let [r, i] = n.split(` `);
			if (r && i && (t[r.toLowerCase()] = Number.parseInt(i, 10)), t.height && t.width) break;
		}
		if (t.height && t.width) return {
			height: t.height,
			width: t.width
		};
		throw TypeError(`Invalid PAM`);
	}
}, R = {
	validate: (e) => t(e, 0, 2) in I,
	calculate(e) {
		let n = t(e, 0, 2), r = I[n], i = t(e, 3).split(/[\n\r]+/);
		return (L[r] || L.default)(i);
	}
}, z = {
	validate: (e) => t(e, 0, 4) === `8BPS`,
	calculate: (e) => ({
		height: c(e, 14),
		width: c(e, 18)
	})
}, B = /<svg\s([^"'>]|"[^"]*"|'[^']*')*>/, V = {
	height: /\sheight=(["'])([^%]+?)\1/,
	root: B,
	viewbox: /\sviewbox=(["'])(.+?)\1/i,
	width: /\swidth=(["'])([^%]+?)\1/
}, H = 2.54, U = {
	in: 96,
	cm: 96 / H,
	em: 16,
	ex: 8,
	m: 96 / H * 100,
	mm: 96 / H / 10,
	pc: 96 / 72 / 12,
	pt: 96 / 72,
	px: 1
}, W = RegExp(`^([0-9.]+(?:e\\d+)?)(${Object.keys(U).join(`|`)})?$`);
function G(e) {
	let t = W.exec(e);
	if (t) return Math.round(Number(t[1]) * (U[t[2]] || 1));
}
function K(e) {
	let t = e.split(` `);
	return {
		height: G(t[3]),
		width: G(t[2])
	};
}
function q(e) {
	let t = e.match(V.width), n = e.match(V.height), r = e.match(V.viewbox);
	return {
		height: n && G(n[2]),
		viewbox: r && K(r[2]),
		width: t && G(t[2])
	};
}
function J(e) {
	return {
		height: e.height,
		width: e.width
	};
}
function Y(e, t) {
	let n = t.width / t.height;
	return e.width ? {
		height: Math.floor(e.width / n),
		width: e.width
	} : e.height ? {
		height: e.height,
		width: Math.floor(e.height * n)
	} : {
		height: t.height,
		width: t.width
	};
}
const ae = {
	validate: (e) => B.test(t(e, 0, 1e3)),
	calculate(e) {
		let n = t(e).match(V.root);
		if (n) {
			let e = q(n[0]);
			if (e.width && e.height) return J(e);
			if (e.viewbox) return Y(e, e.viewbox);
		}
		throw TypeError(`Invalid SVG`);
	}
}, oe = {
	validate(e) {
		return a(e, 0) === 0 && a(e, 4) === 0;
	},
	calculate(e) {
		return {
			height: a(e, 14),
			width: a(e, 12)
		};
	}
};
function se(e, t) {
	let n = d(e, 32, 4, t), r = 1024, i = e.length;
	return n + r > i && (r = i - n - 10), e.slice(n + 2, n + 2 + r);
}
function ce(e, t) {
	let n = d(e, 16, 8, t);
	return (d(e, 16, 10, t) << 16) + n;
}
function le(e) {
	if (e.length > 24) return e.slice(12);
}
function ue(e, t) {
	let n = {}, r = e;
	for (; r && r.length > 0;) {
		let e = d(r, 16, 0, t), i = d(r, 16, 2, t), a = d(r, 32, 4, t);
		if (e === 0) break;
		a === 1 && (i === 3 || i === 4) && (n[e] = ce(r, t)), r = le(r);
	}
	return n;
}
function de(e) {
	let n = t(e, 0, 2);
	if (n === `II`) return `LE`;
	if (n === `MM`) return `BE`;
}
const fe = /* @__PURE__ */ new Set([`49492a00`, `4d4d002a`]), pe = {
	validate: (e) => fe.has(n(e, 0, 4)),
	calculate(e) {
		let t = de(e) === `BE`, n = ue(se(e, t), t), r = n[256], i = n[257];
		if (!r || !i) throw TypeError(`Invalid Tiff. Missing tags`);
		return {
			height: i,
			width: r
		};
	}
};
function me(e) {
	return {
		height: 1 + o(e, 7),
		width: 1 + o(e, 4)
	};
}
function he(e) {
	return {
		height: 1 + ((e[4] & 15) << 10 | e[3] << 2 | (e[2] & 192) >> 6),
		width: 1 + ((e[2] & 63) << 8 | e[1])
	};
}
function ge(e) {
	return {
		height: r(e, 8) & 16383,
		width: r(e, 6) & 16383
	};
}
const X = {
	validate(e) {
		let n = t(e, 0, 4) === `RIFF`, r = t(e, 8, 12) === `WEBP`, i = t(e, 12, 15) === `VP8`;
		return n && r && i;
	},
	calculate(e) {
		let r = t(e, 12, 16);
		if (e = e.slice(20, 30), r === `VP8X`) {
			let t = e[0], n = (t & 192) == 0, r = (t & 1) == 0;
			if (n && r) return me(e);
			throw TypeError(`Invalid WebP`);
		}
		if (r === `VP8 ` && e[0] !== 47) return ge(e);
		let i = n(e, 3, 6);
		if (r === `VP8L` && i !== `9d012a`) return he(e);
		throw TypeError(`Invalid WebP`);
	}
}, _e = {
	validate: (e) => t(e, 8, 12) === `avif`,
	calculate: (e) => {
		let t = Z(e, `meta`), n = Z(e, `iprp`, t.offset + 12, t.offset + t.size), r = Z(e, `ipco`, n.offset + 8, n.offset + n.size), i = Z(e, `ispe`, r.offset + 8, r.offset + r.size);
		return {
			width: c(e, i.offset + 12),
			height: c(e, i.offset + 16)
		};
	}
};
function Z(e, n, r = 0, i = e.length) {
	for (let a = r; a < i;) {
		let r = c(e, a);
		if (t(e, a + 4, a + 8) === n) return {
			offset: a,
			size: r
		};
		if (r <= 0 || a + r > i) break;
		a += r;
	}
	throw Error(`${n} box not found`);
}
const Q = {
	bmp: ee,
	cur: te,
	dds: h,
	gif: _,
	heic: v,
	icns: ne,
	ico: m,
	j2c: re,
	jp2: E,
	jpg: M,
	ktx: N,
	png: F,
	pnm: R,
	psd: z,
	svg: ae,
	tga: oe,
	tiff: pe,
	webp: X,
	avif: _e
}, ve = Object.keys(Q), $ = {
	56: `psd`,
	66: `bmp`,
	68: `dds`,
	71: `gif`,
	73: `tiff`,
	77: `tiff`,
	82: `webp`,
	105: `icns`,
	137: `png`,
	255: `jpg`
};
function ye(e) {
	let t = e[0];
	if (t in $) {
		let n = $[t];
		if (n && Q[n].validate(e)) return n;
	}
	return ve.find((t) => Q[t].validate(e));
}
function be(e) {
	if (!(e instanceof Uint8Array)) throw TypeError(`Input should be a Uint8Array`);
	let t = ye(e);
	if (t !== void 0 && t in Q) {
		let n = Q[t].calculate(e);
		if (n !== void 0) return n.type = t, n;
	}
	throw TypeError(`Unsupported file type: ${t}`);
}
export { be as imageMeta };
