import { __commonJSMin as e, __esmMin as t, __exportAll as n, __toCommonJS as r } from "../rolldown-runtime.mjs";
import { require_boolbase as i } from "./boolbase.mjs";
var a = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.Doctype = e.CDATA = e.Tag = e.Style = e.Script = e.Comment = e.Directive = e.Text = e.Root = e.isTag = e.ElementType = void 0;
	var t;
	(function(e) {
		e.Root = `root`, e.Text = `text`, e.Directive = `directive`, e.Comment = `comment`, e.Script = `script`, e.Style = `style`, e.Tag = `tag`, e.CDATA = `cdata`, e.Doctype = `doctype`;
	})(t = e.ElementType ||= {});
	function n(e) {
		return e.type === t.Tag || e.type === t.Script || e.type === t.Style;
	}
	e.isTag = n, e.Root = t.Root, e.Text = t.Text, e.Directive = t.Directive, e.Comment = t.Comment, e.Script = t.Script, e.Style = t.Style, e.Tag = t.Tag, e.CDATA = t.CDATA, e.Doctype = t.Doctype;
})), o = e(((e) => {
	var t = e && e.__extends || (function() {
		var e = function(t, n) {
			return e = Object.setPrototypeOf || { __proto__: [] } instanceof Array && function(e, t) {
				e.__proto__ = t;
			} || function(e, t) {
				for (var n in t) Object.prototype.hasOwnProperty.call(t, n) && (e[n] = t[n]);
			}, e(t, n);
		};
		return function(t, n) {
			if (typeof n != `function` && n !== null) throw TypeError(`Class extends value ` + String(n) + ` is not a constructor or null`);
			e(t, n);
			function r() {
				this.constructor = t;
			}
			t.prototype = n === null ? Object.create(n) : (r.prototype = n.prototype, new r());
		};
	})(), n = e && e.__assign || function() {
		return n = Object.assign || function(e) {
			for (var t, n = 1, r = arguments.length; n < r; n++) for (var i in t = arguments[n], t) Object.prototype.hasOwnProperty.call(t, i) && (e[i] = t[i]);
			return e;
		}, n.apply(this, arguments);
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.cloneNode = e.hasChildren = e.isDocument = e.isDirective = e.isComment = e.isText = e.isCDATA = e.isTag = e.Element = e.Document = e.CDATA = e.NodeWithChildren = e.ProcessingInstruction = e.Comment = e.Text = e.DataNode = e.Node = void 0;
	var r = a(), i = function() {
		function e() {
			this.parent = null, this.prev = null, this.next = null, this.startIndex = null, this.endIndex = null;
		}
		return Object.defineProperty(e.prototype, "parentNode", {
			get: function() {
				return this.parent;
			},
			set: function(e) {
				this.parent = e;
			},
			enumerable: !1,
			configurable: !0
		}), Object.defineProperty(e.prototype, "previousSibling", {
			get: function() {
				return this.prev;
			},
			set: function(e) {
				this.prev = e;
			},
			enumerable: !1,
			configurable: !0
		}), Object.defineProperty(e.prototype, "nextSibling", {
			get: function() {
				return this.next;
			},
			set: function(e) {
				this.next = e;
			},
			enumerable: !1,
			configurable: !0
		}), e.prototype.cloneNode = function(e) {
			return e === void 0 && (e = !1), x(this, e);
		}, e;
	}();
	e.Node = i;
	var o = function(e) {
		t(n, e);
		function n(t) {
			var n = e.call(this) || this;
			return n.data = t, n;
		}
		return Object.defineProperty(n.prototype, "nodeValue", {
			get: function() {
				return this.data;
			},
			set: function(e) {
				this.data = e;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(i);
	e.DataNode = o;
	var s = function(e) {
		t(n, e);
		function n() {
			var t = e !== null && e.apply(this, arguments) || this;
			return t.type = r.ElementType.Text, t;
		}
		return Object.defineProperty(n.prototype, "nodeType", {
			get: function() {
				return 3;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(o);
	e.Text = s;
	var c = function(e) {
		t(n, e);
		function n() {
			var t = e !== null && e.apply(this, arguments) || this;
			return t.type = r.ElementType.Comment, t;
		}
		return Object.defineProperty(n.prototype, "nodeType", {
			get: function() {
				return 8;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(o);
	e.Comment = c;
	var l = function(e) {
		t(n, e);
		function n(t, n) {
			var i = e.call(this, n) || this;
			return i.name = t, i.type = r.ElementType.Directive, i;
		}
		return Object.defineProperty(n.prototype, "nodeType", {
			get: function() {
				return 1;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(o);
	e.ProcessingInstruction = l;
	var u = function(e) {
		t(n, e);
		function n(t) {
			var n = e.call(this) || this;
			return n.children = t, n;
		}
		return Object.defineProperty(n.prototype, "firstChild", {
			get: function() {
				return this.children[0] ?? null;
			},
			enumerable: !1,
			configurable: !0
		}), Object.defineProperty(n.prototype, "lastChild", {
			get: function() {
				return this.children.length > 0 ? this.children[this.children.length - 1] : null;
			},
			enumerable: !1,
			configurable: !0
		}), Object.defineProperty(n.prototype, "childNodes", {
			get: function() {
				return this.children;
			},
			set: function(e) {
				this.children = e;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(i);
	e.NodeWithChildren = u;
	var d = function(e) {
		t(n, e);
		function n() {
			var t = e !== null && e.apply(this, arguments) || this;
			return t.type = r.ElementType.CDATA, t;
		}
		return Object.defineProperty(n.prototype, "nodeType", {
			get: function() {
				return 4;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(u);
	e.CDATA = d;
	var f = function(e) {
		t(n, e);
		function n() {
			var t = e !== null && e.apply(this, arguments) || this;
			return t.type = r.ElementType.Root, t;
		}
		return Object.defineProperty(n.prototype, "nodeType", {
			get: function() {
				return 9;
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(u);
	e.Document = f;
	var p = function(e) {
		t(n, e);
		function n(t, n, i, a) {
			i === void 0 && (i = []), a === void 0 && (a = t === `script` ? r.ElementType.Script : t === `style` ? r.ElementType.Style : r.ElementType.Tag);
			var o = e.call(this, i) || this;
			return o.name = t, o.attribs = n, o.type = a, o;
		}
		return Object.defineProperty(n.prototype, "nodeType", {
			get: function() {
				return 1;
			},
			enumerable: !1,
			configurable: !0
		}), Object.defineProperty(n.prototype, "tagName", {
			get: function() {
				return this.name;
			},
			set: function(e) {
				this.name = e;
			},
			enumerable: !1,
			configurable: !0
		}), Object.defineProperty(n.prototype, "attributes", {
			get: function() {
				var e = this;
				return Object.keys(this.attribs).map(function(t) {
					return {
						name: t,
						value: e.attribs[t],
						namespace: e[`x-attribsNamespace`]?.[t],
						prefix: e[`x-attribsPrefix`]?.[t]
					};
				});
			},
			enumerable: !1,
			configurable: !0
		}), n;
	}(u);
	e.Element = p;
	function m(e) {
		return (0, r.isTag)(e);
	}
	e.isTag = m;
	function h(e) {
		return e.type === r.ElementType.CDATA;
	}
	e.isCDATA = h;
	function g(e) {
		return e.type === r.ElementType.Text;
	}
	e.isText = g;
	function _(e) {
		return e.type === r.ElementType.Comment;
	}
	e.isComment = _;
	function v(e) {
		return e.type === r.ElementType.Directive;
	}
	e.isDirective = v;
	function y(e) {
		return e.type === r.ElementType.Root;
	}
	e.isDocument = y;
	function b(e) {
		return Object.prototype.hasOwnProperty.call(e, `children`);
	}
	e.hasChildren = b;
	function x(e, t) {
		t === void 0 && (t = !1);
		var r;
		if (g(e)) r = new s(e.data);
		else if (_(e)) r = new c(e.data);
		else if (m(e)) {
			var i = t ? S(e.children) : [], a = new p(e.name, n({}, e.attribs), i);
			i.forEach(function(e) {
				return e.parent = a;
			}), e.namespace != null && (a.namespace = e.namespace), e[`x-attribsNamespace`] && (a[`x-attribsNamespace`] = n({}, e[`x-attribsNamespace`])), e[`x-attribsPrefix`] && (a[`x-attribsPrefix`] = n({}, e[`x-attribsPrefix`])), r = a;
		} else if (h(e)) {
			var i = t ? S(e.children) : [], o = new d(i);
			i.forEach(function(e) {
				return e.parent = o;
			}), r = o;
		} else if (y(e)) {
			var i = t ? S(e.children) : [], u = new f(i);
			i.forEach(function(e) {
				return e.parent = u;
			}), e[`x-mode`] && (u[`x-mode`] = e[`x-mode`]), r = u;
		} else if (v(e)) {
			var b = new l(e.name, e.data);
			e[`x-name`] != null && (b[`x-name`] = e[`x-name`], b[`x-publicId`] = e[`x-publicId`], b[`x-systemId`] = e[`x-systemId`]), r = b;
		} else throw Error(`Not implemented yet: ${e.type}`);
		return r.startIndex = e.startIndex, r.endIndex = e.endIndex, e.sourceCodeLocation != null && (r.sourceCodeLocation = e.sourceCodeLocation), r;
	}
	e.cloneNode = x;
	function S(e) {
		for (var t = e.map(function(e) {
			return x(e, !0);
		}), n = 1; n < t.length; n++) t[n].prev = t[n - 1], t[n - 1].next = t[n];
		return t;
	}
})), s = e(((e) => {
	var t = e && e.__createBinding || (Object.create ? (function(e, t, n, r) {
		r === void 0 && (r = n);
		var i = Object.getOwnPropertyDescriptor(t, n);
		(!i || (`get` in i ? !t.__esModule : i.writable || i.configurable)) && (i = {
			enumerable: !0,
			get: function() {
				return t[n];
			}
		}), Object.defineProperty(e, r, i);
	}) : (function(e, t, n, r) {
		r === void 0 && (r = n), e[r] = t[n];
	})), n = e && e.__exportStar || function(e, n) {
		for (var r in e) r !== "default" && !Object.prototype.hasOwnProperty.call(n, r) && t(n, e, r);
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.DomHandler = void 0;
	var r = a(), i = o();
	n(o(), e);
	var s = {
		withStartIndices: !1,
		withEndIndices: !1,
		xmlMode: !1
	}, c = function() {
		function e(e, t, n) {
			this.dom = [], this.root = new i.Document(this.dom), this.done = !1, this.tagStack = [this.root], this.lastNode = null, this.parser = null, typeof t == `function` && (n = t, t = s), typeof e == `object` && (t = e, e = void 0), this.callback = e ?? null, this.options = t ?? s, this.elementCB = n ?? null;
		}
		return e.prototype.onparserinit = function(e) {
			this.parser = e;
		}, e.prototype.onreset = function() {
			this.dom = [], this.root = new i.Document(this.dom), this.done = !1, this.tagStack = [this.root], this.lastNode = null, this.parser = null;
		}, e.prototype.onend = function() {
			this.done || (this.done = !0, this.parser = null, this.handleCallback(null));
		}, e.prototype.onerror = function(e) {
			this.handleCallback(e);
		}, e.prototype.onclosetag = function() {
			this.lastNode = null;
			var e = this.tagStack.pop();
			this.options.withEndIndices && (e.endIndex = this.parser.endIndex), this.elementCB && this.elementCB(e);
		}, e.prototype.onopentag = function(e, t) {
			var n = this.options.xmlMode ? r.ElementType.Tag : void 0, a = new i.Element(e, t, void 0, n);
			this.addNode(a), this.tagStack.push(a);
		}, e.prototype.ontext = function(e) {
			var t = this.lastNode;
			if (t && t.type === r.ElementType.Text) t.data += e, this.options.withEndIndices && (t.endIndex = this.parser.endIndex);
			else {
				var n = new i.Text(e);
				this.addNode(n), this.lastNode = n;
			}
		}, e.prototype.oncomment = function(e) {
			if (this.lastNode && this.lastNode.type === r.ElementType.Comment) {
				this.lastNode.data += e;
				return;
			}
			var t = new i.Comment(e);
			this.addNode(t), this.lastNode = t;
		}, e.prototype.oncommentend = function() {
			this.lastNode = null;
		}, e.prototype.oncdatastart = function() {
			var e = new i.Text(``), t = new i.CDATA([e]);
			this.addNode(t), e.parent = t, this.lastNode = e;
		}, e.prototype.oncdataend = function() {
			this.lastNode = null;
		}, e.prototype.onprocessinginstruction = function(e, t) {
			var n = new i.ProcessingInstruction(e, t);
			this.addNode(n);
		}, e.prototype.handleCallback = function(e) {
			if (typeof this.callback == `function`) this.callback(e, this.dom);
			else if (e) throw e;
		}, e.prototype.addNode = function(e) {
			var t = this.tagStack[this.tagStack.length - 1], n = t.children[t.children.length - 1];
			this.options.withStartIndices && (e.startIndex = this.parser.startIndex), this.options.withEndIndices && (e.endIndex = this.parser.endIndex), t.children.push(e), n && (e.prev = n, n.next = e), e.parent = t, this.lastNode = null;
		}, e;
	}();
	e.DomHandler = c, e.default = c;
})), c = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.default = new Uint16Array(`ᵁ<Õıʊҝջאٵ۞ޢߖࠏ੊ઑඡ๭༉༦჊ረዡᐕᒝᓃᓟᔥ\0\0\0\0\0\0ᕫᛍᦍᰒᷝ὾⁠↰⊍⏀⏻⑂⠤⤒ⴈ⹈⿎〖㊺㘹㞬㣾㨨㩱㫠㬮ࠀEMabcfglmnoprstu\\bfms¦³¹ÈÏlig耻Æ䃆P耻&䀦cute耻Á䃁reve;䄂Āiyx}rc耻Â䃂;䐐r;쀀𝔄rave耻À䃀pha;䎑acr;䄀d;橓Āgp¡on;䄄f;쀀𝔸plyFunction;恡ing耻Å䃅Ācs¾Ãr;쀀𝒜ign;扔ilde耻Ã䃃ml耻Ä䃄ЀaceforsuåûþėĜĢħĪĀcrêòkslash;或Ŷöø;櫧ed;挆y;䐑ƀcrtąċĔause;戵noullis;愬a;䎒r;쀀𝔅pf;쀀𝔹eve;䋘còēmpeq;扎܀HOacdefhilorsuōőŖƀƞƢƵƷƺǜȕɳɸɾcy;䐧PY耻©䂩ƀcpyŝŢźute;䄆Ā;iŧŨ拒talDifferentialD;慅leys;愭ȀaeioƉƎƔƘron;䄌dil耻Ç䃇rc;䄈nint;戰ot;䄊ĀdnƧƭilla;䂸terDot;䂷òſi;䎧rcleȀDMPTǇǋǑǖot;抙inus;抖lus;投imes;抗oĀcsǢǸkwiseContourIntegral;戲eCurlyĀDQȃȏoubleQuote;思uote;怙ȀlnpuȞȨɇɕonĀ;eȥȦ户;橴ƀgitȯȶȺruent;扡nt;戯ourIntegral;戮ĀfrɌɎ;愂oduct;成nterClockwiseContourIntegral;戳oss;樯cr;쀀𝒞pĀ;Cʄʅ拓ap;才րDJSZacefiosʠʬʰʴʸˋ˗ˡ˦̳ҍĀ;oŹʥtrahd;椑cy;䐂cy;䐅cy;䐏ƀgrsʿ˄ˇger;怡r;憡hv;櫤Āayː˕ron;䄎;䐔lĀ;t˝˞戇a;䎔r;쀀𝔇Āaf˫̧Ācm˰̢riticalȀADGT̖̜̀̆cute;䂴oŴ̋̍;䋙bleAcute;䋝rave;䁠ilde;䋜ond;拄ferentialD;慆Ѱ̽\0\0\0͔͂\0Ѕf;쀀𝔻ƀ;DE͈͉͍䂨ot;惜qual;扐blèCDLRUVͣͲ΂ϏϢϸontourIntegraìȹoɴ͹\0\0ͻ»͉nArrow;懓Āeo·ΤftƀARTΐΖΡrrow;懐ightArrow;懔eåˊngĀLRΫτeftĀARγιrrow;柸ightArrow;柺ightArrow;柹ightĀATϘϞrrow;懒ee;抨pɁϩ\0\0ϯrrow;懑ownArrow;懕erticalBar;戥ǹABLRTaВЪаўѿͼrrowƀ;BUНОТ憓ar;椓pArrow;懵reve;䌑eft˒к\0ц\0ѐightVector;楐eeVector;楞ectorĀ;Bљњ憽ar;楖ightǔѧ\0ѱeeVector;楟ectorĀ;BѺѻ懁ar;楗eeĀ;A҆҇护rrow;憧ĀctҒҗr;쀀𝒟rok;䄐ࠀNTacdfglmopqstuxҽӀӄӋӞӢӧӮӵԡԯԶՒ՝ՠեG;䅊H耻Ð䃐cute耻É䃉ƀaiyӒӗӜron;䄚rc耻Ê䃊;䐭ot;䄖r;쀀𝔈rave耻È䃈ement;戈ĀapӺӾcr;䄒tyɓԆ\0\0ԒmallSquare;旻erySmallSquare;斫ĀgpԦԪon;䄘f;쀀𝔼silon;䎕uĀaiԼՉlĀ;TՂՃ橵ilde;扂librium;懌Āci՗՚r;愰m;橳a;䎗ml耻Ë䃋Āipժկsts;戃onentialE;慇ʀcfiosօֈ֍ֲ׌y;䐤r;쀀𝔉lledɓ֗\0\0֣mallSquare;旼erySmallSquare;斪Ͱֺ\0ֿ\0\0ׄf;쀀𝔽All;戀riertrf;愱cò׋؀JTabcdfgorstר׬ׯ׺؀ؒؖ؛؝أ٬ٲcy;䐃耻>䀾mmaĀ;d׷׸䎓;䏜reve;䄞ƀeiy؇،ؐdil;䄢rc;䄜;䐓ot;䄠r;쀀𝔊;拙pf;쀀𝔾eater̀EFGLSTصلَٖٛ٦qualĀ;Lؾؿ扥ess;招ullEqual;执reater;檢ess;扷lantEqual;橾ilde;扳cr;쀀𝒢;扫ЀAacfiosuڅڋږڛڞڪھۊRDcy;䐪Āctڐڔek;䋇;䁞irc;䄤r;愌lbertSpace;愋ǰگ\0ڲf;愍izontalLine;攀Āctۃۅòکrok;䄦mpńېۘownHumðįqual;扏܀EJOacdfgmnostuۺ۾܃܇܎ܚܞܡܨ݄ݸދޏޕcy;䐕lig;䄲cy;䐁cute耻Í䃍Āiyܓܘrc耻Î䃎;䐘ot;䄰r;愑rave耻Ì䃌ƀ;apܠܯܿĀcgܴܷr;䄪inaryI;慈lieóϝǴ݉\0ݢĀ;eݍݎ戬Āgrݓݘral;戫section;拂isibleĀCTݬݲomma;恣imes;恢ƀgptݿރވon;䄮f;쀀𝕀a;䎙cr;愐ilde;䄨ǫޚ\0ޞcy;䐆l耻Ï䃏ʀcfosuެ޷޼߂ߐĀiyޱ޵rc;䄴;䐙r;쀀𝔍pf;쀀𝕁ǣ߇\0ߌr;쀀𝒥rcy;䐈kcy;䐄΀HJacfosߤߨ߽߬߱ࠂࠈcy;䐥cy;䐌ppa;䎚Āey߶߻dil;䄶;䐚r;쀀𝔎pf;쀀𝕂cr;쀀𝒦րJTaceflmostࠥࠩࠬࡐࡣ঳সে্਷ੇcy;䐉耻<䀼ʀcmnpr࠷࠼ࡁࡄࡍute;䄹bda;䎛g;柪lacetrf;愒r;憞ƀaeyࡗ࡜ࡡron;䄽dil;䄻;䐛Āfsࡨ॰tԀACDFRTUVarࡾࢩࢱࣦ࣠ࣼयज़ΐ४Ānrࢃ࢏gleBracket;柨rowƀ;BR࢙࢚࢞憐ar;懤ightArrow;懆eiling;挈oǵࢷ\0ࣃbleBracket;柦nǔࣈ\0࣒eeVector;楡ectorĀ;Bࣛࣜ懃ar;楙loor;挊ightĀAV࣯ࣵrrow;憔ector;楎Āerँगeƀ;AVउऊऐ抣rrow;憤ector;楚iangleƀ;BEतथऩ抲ar;槏qual;抴pƀDTVषूौownVector;楑eeVector;楠ectorĀ;Bॖॗ憿ar;楘ectorĀ;B॥०憼ar;楒ightáΜs̀EFGLSTॾঋকঝঢভqualGreater;拚ullEqual;扦reater;扶ess;檡lantEqual;橽ilde;扲r;쀀𝔏Ā;eঽা拘ftarrow;懚idot;䄿ƀnpw৔ਖਛgȀLRlr৞৷ਂਐeftĀAR০৬rrow;柵ightArrow;柷ightArrow;柶eftĀarγਊightáοightáϊf;쀀𝕃erĀLRਢਬeftArrow;憙ightArrow;憘ƀchtਾੀੂòࡌ;憰rok;䅁;扪Ѐacefiosuਗ਼੝੠੷੼અઋ઎p;椅y;䐜Ādl੥੯iumSpace;恟lintrf;愳r;쀀𝔐nusPlus;戓pf;쀀𝕄cò੶;䎜ҀJacefostuણધભીଔଙඑ඗ඞcy;䐊cute;䅃ƀaey઴હાron;䅇dil;䅅;䐝ƀgswે૰଎ativeƀMTV૓૟૨ediumSpace;怋hiĀcn૦૘ë૙eryThiî૙tedĀGL૸ଆreaterGreateòٳessLesóੈLine;䀊r;쀀𝔑ȀBnptଢନଷ଺reak;恠BreakingSpace;䂠f;愕ڀ;CDEGHLNPRSTV୕ୖ୪୼஡௫ఄ౞಄ದ೘ൡඅ櫬Āou୛୤ngruent;扢pCap;扭oubleVerticalBar;戦ƀlqxஃஊ஛ement;戉ualĀ;Tஒஓ扠ilde;쀀≂̸ists;戄reater΀;EFGLSTஶஷ஽௉௓௘௥扯qual;扱ullEqual;쀀≧̸reater;쀀≫̸ess;批lantEqual;쀀⩾̸ilde;扵umpń௲௽ownHump;쀀≎̸qual;쀀≏̸eĀfsఊధtTriangleƀ;BEచఛడ拪ar;쀀⧏̸qual;括s̀;EGLSTవశ఼ౄోౘ扮qual;扰reater;扸ess;쀀≪̸lantEqual;쀀⩽̸ilde;扴estedĀGL౨౹reaterGreater;쀀⪢̸essLess;쀀⪡̸recedesƀ;ESಒಓಛ技qual;쀀⪯̸lantEqual;拠ĀeiಫಹverseElement;戌ghtTriangleƀ;BEೋೌ೒拫ar;쀀⧐̸qual;拭ĀquೝഌuareSuĀbp೨೹setĀ;E೰ೳ쀀⊏̸qual;拢ersetĀ;Eഃആ쀀⊐̸qual;拣ƀbcpഓതൎsetĀ;Eഛഞ쀀⊂⃒qual;抈ceedsȀ;ESTലള഻െ抁qual;쀀⪰̸lantEqual;拡ilde;쀀≿̸ersetĀ;E൘൛쀀⊃⃒qual;抉ildeȀ;EFT൮൯൵ൿ扁qual;扄ullEqual;扇ilde;扉erticalBar;戤cr;쀀𝒩ilde耻Ñ䃑;䎝܀Eacdfgmoprstuvලෂ෉෕ෛ෠෧෼ขภยา฿ไlig;䅒cute耻Ó䃓Āiy෎ීrc耻Ô䃔;䐞blac;䅐r;쀀𝔒rave耻Ò䃒ƀaei෮ෲ෶cr;䅌ga;䎩cron;䎟pf;쀀𝕆enCurlyĀDQฎบoubleQuote;怜uote;怘;橔Āclวฬr;쀀𝒪ash耻Ø䃘iŬื฼de耻Õ䃕es;樷ml耻Ö䃖erĀBP๋๠Āar๐๓r;怾acĀek๚๜;揞et;掴arenthesis;揜Ҁacfhilors๿ງຊຏຒດຝະ໼rtialD;戂y;䐟r;쀀𝔓i;䎦;䎠usMinus;䂱Āipຢອncareplanåڝf;愙Ȁ;eio຺ູ໠໤檻cedesȀ;EST່້໏໚扺qual;檯lantEqual;扼ilde;找me;怳Ādp໩໮uct;戏ortionĀ;aȥ໹l;戝Āci༁༆r;쀀𝒫;䎨ȀUfos༑༖༛༟OT耻"䀢r;쀀𝔔pf;愚cr;쀀𝒬؀BEacefhiorsu༾གྷཇའཱིྦྷྪྭ႖ႩႴႾarr;椐G耻®䂮ƀcnrཎནབute;䅔g;柫rĀ;tཛྷཝ憠l;椖ƀaeyཧཬཱron;䅘dil;䅖;䐠Ā;vླྀཹ愜erseĀEUྂྙĀlq྇ྎement;戋uilibrium;懋pEquilibrium;楯r»ཹo;䎡ghtЀACDFTUVa࿁࿫࿳ဢဨၛႇϘĀnr࿆࿒gleBracket;柩rowƀ;BL࿜࿝࿡憒ar;懥eftArrow;懄eiling;按oǵ࿹\0စbleBracket;柧nǔည\0နeeVector;楝ectorĀ;Bဝသ懂ar;楕loor;挋Āerိ၃eƀ;AVဵံြ抢rrow;憦ector;楛iangleƀ;BEၐၑၕ抳ar;槐qual;抵pƀDTVၣၮၸownVector;楏eeVector;楜ectorĀ;Bႂႃ憾ar;楔ectorĀ;B႑႒懀ar;楓Āpuႛ႞f;愝ndImplies;楰ightarrow;懛ĀchႹႼr;愛;憱leDelayed;槴ڀHOacfhimoqstuფჱჷჽᄙᄞᅑᅖᅡᅧᆵᆻᆿĀCcჩხHcy;䐩y;䐨FTcy;䐬cute;䅚ʀ;aeiyᄈᄉᄎᄓᄗ檼ron;䅠dil;䅞rc;䅜;䐡r;쀀𝔖ortȀDLRUᄪᄴᄾᅉownArrow»ОeftArrow»࢚ightArrow»࿝pArrow;憑gma;䎣allCircle;战pf;쀀𝕊ɲᅭ\0\0ᅰt;戚areȀ;ISUᅻᅼᆉᆯ斡ntersection;抓uĀbpᆏᆞsetĀ;Eᆗᆘ抏qual;抑ersetĀ;Eᆨᆩ抐qual;抒nion;抔cr;쀀𝒮ar;拆ȀbcmpᇈᇛሉላĀ;sᇍᇎ拐etĀ;Eᇍᇕqual;抆ĀchᇠህeedsȀ;ESTᇭᇮᇴᇿ扻qual;檰lantEqual;扽ilde;承Tháྌ;我ƀ;esሒሓሣ拑rsetĀ;Eሜም抃qual;抇et»ሓրHRSacfhiorsሾቄ቉ቕ቞ቱቶኟዂወዑORN耻Þ䃞ADE;愢ĀHc቎ቒcy;䐋y;䐦Ābuቚቜ;䀉;䎤ƀaeyብቪቯron;䅤dil;䅢;䐢r;쀀𝔗Āeiቻ኉ǲኀ\0ኇefore;戴a;䎘Ācn኎ኘkSpace;쀀  Space;怉ldeȀ;EFTካኬኲኼ戼qual;扃ullEqual;扅ilde;扈pf;쀀𝕋ipleDot;惛Āctዖዛr;쀀𝒯rok;䅦ૡዷጎጚጦ\0ጬጱ\0\0\0\0\0ጸጽ፷ᎅ\0᏿ᐄᐊᐐĀcrዻጁute耻Ú䃚rĀ;oጇገ憟cir;楉rǣጓ\0጖y;䐎ve;䅬Āiyጞጣrc耻Û䃛;䐣blac;䅰r;쀀𝔘rave耻Ù䃙acr;䅪Ādiፁ፩erĀBPፈ፝Āarፍፐr;䁟acĀekፗፙ;揟et;掵arenthesis;揝onĀ;P፰፱拃lus;抎Āgp፻፿on;䅲f;쀀𝕌ЀADETadps᎕ᎮᎸᏄϨᏒᏗᏳrrowƀ;BDᅐᎠᎤar;椒ownArrow;懅ownArrow;憕quilibrium;楮eeĀ;AᏋᏌ报rrow;憥ownáϳerĀLRᏞᏨeftArrow;憖ightArrow;憗iĀ;lᏹᏺ䏒on;䎥ing;䅮cr;쀀𝒰ilde;䅨ml耻Ü䃜ҀDbcdefosvᐧᐬᐰᐳᐾᒅᒊᒐᒖash;披ar;櫫y;䐒ashĀ;lᐻᐼ抩;櫦Āerᑃᑅ;拁ƀbtyᑌᑐᑺar;怖Ā;iᑏᑕcalȀBLSTᑡᑥᑪᑴar;戣ine;䁼eparator;杘ilde;所ThinSpace;怊r;쀀𝔙pf;쀀𝕍cr;쀀𝒱dash;抪ʀcefosᒧᒬᒱᒶᒼirc;䅴dge;拀r;쀀𝔚pf;쀀𝕎cr;쀀𝒲Ȁfiosᓋᓐᓒᓘr;쀀𝔛;䎞pf;쀀𝕏cr;쀀𝒳ҀAIUacfosuᓱᓵᓹᓽᔄᔏᔔᔚᔠcy;䐯cy;䐇cy;䐮cute耻Ý䃝Āiyᔉᔍrc;䅶;䐫r;쀀𝔜pf;쀀𝕐cr;쀀𝒴ml;䅸ЀHacdefosᔵᔹᔿᕋᕏᕝᕠᕤcy;䐖cute;䅹Āayᕄᕉron;䅽;䐗ot;䅻ǲᕔ\0ᕛoWidtè૙a;䎖r;愨pf;愤cr;쀀𝒵௡ᖃᖊᖐ\0ᖰᖶᖿ\0\0\0\0ᗆᗛᗫᙟ᙭\0ᚕ᚛ᚲᚹ\0ᚾcute耻á䃡reve;䄃̀;Ediuyᖜᖝᖡᖣᖨᖭ戾;쀀∾̳;房rc耻â䃢te肻´̆;䐰lig耻æ䃦Ā;r²ᖺ;쀀𝔞rave耻à䃠ĀepᗊᗖĀfpᗏᗔsym;愵èᗓha;䎱ĀapᗟcĀclᗤᗧr;䄁g;樿ɤᗰ\0\0ᘊʀ;adsvᗺᗻᗿᘁᘇ戧nd;橕;橜lope;橘;橚΀;elmrszᘘᘙᘛᘞᘿᙏᙙ戠;榤e»ᘙsdĀ;aᘥᘦ戡ѡᘰᘲᘴᘶᘸᘺᘼᘾ;榨;榩;榪;榫;榬;榭;榮;榯tĀ;vᙅᙆ戟bĀ;dᙌᙍ抾;榝Āptᙔᙗh;戢»¹arr;捼Āgpᙣᙧon;䄅f;쀀𝕒΀;Eaeiop዁ᙻᙽᚂᚄᚇᚊ;橰cir;橯;扊d;手s;䀧roxĀ;e዁ᚒñᚃing耻å䃥ƀctyᚡᚦᚨr;쀀𝒶;䀪mpĀ;e዁ᚯñʈilde耻ã䃣ml耻ä䃤Āciᛂᛈoninôɲnt;樑ࠀNabcdefiklnoprsu᛭ᛱᜰ᜼ᝃᝈ᝸᝽០៦ᠹᡐᜍ᤽᥈ᥰot;櫭Ācrᛶ᜞kȀcepsᜀᜅᜍᜓong;扌psilon;䏶rime;怵imĀ;e᜚᜛戽q;拍Ŷᜢᜦee;抽edĀ;gᜬᜭ挅e»ᜭrkĀ;t፜᜷brk;掶Āoyᜁᝁ;䐱quo;怞ʀcmprtᝓ᝛ᝡᝤᝨausĀ;eĊĉptyv;榰séᜌnoõēƀahwᝯ᝱ᝳ;䎲;愶een;扬r;쀀𝔟g΀costuvwឍឝឳេ៕៛៞ƀaiuបពរðݠrc;旯p»፱ƀdptឤឨឭot;樀lus;樁imes;樂ɱឹ\0\0ើcup;樆ar;昅riangleĀdu៍្own;施p;斳plus;樄eåᑄåᒭarow;植ƀako៭ᠦᠵĀcn៲ᠣkƀlst៺֫᠂ozenge;槫riangleȀ;dlr᠒᠓᠘᠝斴own;斾eft;旂ight;斸k;搣Ʊᠫ\0ᠳƲᠯ\0ᠱ;斒;斑4;斓ck;斈ĀeoᠾᡍĀ;qᡃᡆ쀀=⃥uiv;쀀≡⃥t;挐Ȁptwxᡙᡞᡧᡬf;쀀𝕓Ā;tᏋᡣom»Ꮜtie;拈؀DHUVbdhmptuvᢅᢖᢪᢻᣗᣛᣬ᣿ᤅᤊᤐᤡȀLRlrᢎᢐᢒᢔ;敗;敔;敖;敓ʀ;DUduᢡᢢᢤᢦᢨ敐;敦;敩;敤;敧ȀLRlrᢳᢵᢷᢹ;敝;敚;敜;教΀;HLRhlrᣊᣋᣍᣏᣑᣓᣕ救;敬;散;敠;敫;敢;敟ox;槉ȀLRlrᣤᣦᣨᣪ;敕;敒;攐;攌ʀ;DUduڽ᣷᣹᣻᣽;敥;敨;攬;攴inus;抟lus;択imes;抠ȀLRlrᤙᤛᤝ᤟;敛;敘;攘;攔΀;HLRhlrᤰᤱᤳᤵᤷ᤻᤹攂;敪;敡;敞;攼;攤;攜Āevģ᥂bar耻¦䂦Ȁceioᥑᥖᥚᥠr;쀀𝒷mi;恏mĀ;e᜚᜜lƀ;bhᥨᥩᥫ䁜;槅sub;柈Ŭᥴ᥾lĀ;e᥹᥺怢t»᥺pƀ;Eeįᦅᦇ;檮Ā;qۜۛೡᦧ\0᧨ᨑᨕᨲ\0ᨷᩐ\0\0᪴\0\0᫁\0\0ᬡᬮ᭍᭒\0᯽\0ᰌƀcpr᦭ᦲ᧝ute;䄇̀;abcdsᦿᧀᧄ᧊᧕᧙戩nd;橄rcup;橉Āau᧏᧒p;橋p;橇ot;橀;쀀∩︀Āeo᧢᧥t;恁îړȀaeiu᧰᧻ᨁᨅǰ᧵\0᧸s;橍on;䄍dil耻ç䃧rc;䄉psĀ;sᨌᨍ橌m;橐ot;䄋ƀdmnᨛᨠᨦil肻¸ƭptyv;榲t脀¢;eᨭᨮ䂢räƲr;쀀𝔠ƀceiᨽᩀᩍy;䑇ckĀ;mᩇᩈ朓ark»ᩈ;䏇r΀;Ecefms᩟᩠ᩢᩫ᪤᪪᪮旋;槃ƀ;elᩩᩪᩭ䋆q;扗eɡᩴ\0\0᪈rrowĀlr᩼᪁eft;憺ight;憻ʀRSacd᪒᪔᪖᪚᪟»ཇ;擈st;抛irc;抚ash;抝nint;樐id;櫯cir;槂ubsĀ;u᪻᪼晣it»᪼ˬ᫇᫔᫺\0ᬊonĀ;eᫍᫎ䀺Ā;qÇÆɭ᫙\0\0᫢aĀ;t᫞᫟䀬;䁀ƀ;fl᫨᫩᫫戁îᅠeĀmx᫱᫶ent»᫩eóɍǧ᫾\0ᬇĀ;dኻᬂot;橭nôɆƀfryᬐᬔᬗ;쀀𝕔oäɔ脀©;sŕᬝr;愗Āaoᬥᬩrr;憵ss;朗Ācuᬲᬷr;쀀𝒸Ābpᬼ᭄Ā;eᭁᭂ櫏;櫑Ā;eᭉᭊ櫐;櫒dot;拯΀delprvw᭠᭬᭷ᮂᮬᯔ᯹arrĀlr᭨᭪;椸;椵ɰ᭲\0\0᭵r;拞c;拟arrĀ;p᭿ᮀ憶;椽̀;bcdosᮏᮐᮖᮡᮥᮨ截rcap;橈Āauᮛᮞp;橆p;橊ot;抍r;橅;쀀∪︀Ȁalrv᮵ᮿᯞᯣrrĀ;mᮼᮽ憷;椼yƀevwᯇᯔᯘqɰᯎ\0\0ᯒreã᭳uã᭵ee;拎edge;拏en耻¤䂤earrowĀlrᯮ᯳eft»ᮀight»ᮽeäᯝĀciᰁᰇoninôǷnt;戱lcty;挭ঀAHabcdefhijlorstuwz᰸᰻᰿ᱝᱩᱵᲊᲞᲬᲷ᳻᳿ᴍᵻᶑᶫᶻ᷆᷍rò΁ar;楥Ȁglrs᱈ᱍ᱒᱔ger;怠eth;愸òᄳhĀ;vᱚᱛ怐»ऊūᱡᱧarow;椏aã̕Āayᱮᱳron;䄏;䐴ƀ;ao̲ᱼᲄĀgrʿᲁr;懊tseq;橷ƀglmᲑᲔᲘ耻°䂰ta;䎴ptyv;榱ĀirᲣᲨsht;楿;쀀𝔡arĀlrᲳᲵ»ࣜ»သʀaegsv᳂͸᳖᳜᳠mƀ;oș᳊᳔ndĀ;ș᳑uit;晦amma;䏝in;拲ƀ;io᳧᳨᳸䃷de脀÷;o᳧ᳰntimes;拇nø᳷cy;䑒cɯᴆ\0\0ᴊrn;挞op;挍ʀlptuwᴘᴝᴢᵉᵕlar;䀤f;쀀𝕕ʀ;emps̋ᴭᴷᴽᵂqĀ;d͒ᴳot;扑inus;戸lus;戔quare;抡blebarwedgåúnƀadhᄮᵝᵧownarrowóᲃarpoonĀlrᵲᵶefôᲴighôᲶŢᵿᶅkaro÷གɯᶊ\0\0ᶎrn;挟op;挌ƀcotᶘᶣᶦĀryᶝᶡ;쀀𝒹;䑕l;槶rok;䄑Ādrᶰᶴot;拱iĀ;fᶺ᠖斿Āah᷀᷃ròЩaòྦangle;榦Āci᷒ᷕy;䑟grarr;柿ऀDacdefglmnopqrstuxḁḉḙḸոḼṉṡṾấắẽỡἪἷὄ὎὚ĀDoḆᴴoôᲉĀcsḎḔute耻é䃩ter;橮ȀaioyḢḧḱḶron;䄛rĀ;cḭḮ扖耻ê䃪lon;払;䑍ot;䄗ĀDrṁṅot;扒;쀀𝔢ƀ;rsṐṑṗ檚ave耻è䃨Ā;dṜṝ檖ot;檘Ȁ;ilsṪṫṲṴ檙nters;揧;愓Ā;dṹṺ檕ot;檗ƀapsẅẉẗcr;䄓tyƀ;svẒẓẕ戅et»ẓpĀ1;ẝẤĳạả;怄;怅怃ĀgsẪẬ;䅋p;怂ĀgpẴẸon;䄙f;쀀𝕖ƀalsỄỎỒrĀ;sỊị拕l;槣us;橱iƀ;lvỚớở䎵on»ớ;䏵ȀcsuvỪỳἋἣĀioữḱrc»Ḯɩỹ\0\0ỻíՈantĀglἂἆtr»ṝess»Ṻƀaeiἒ἖Ἒls;䀽st;扟vĀ;DȵἠD;橸parsl;槥ĀDaἯἳot;打rr;楱ƀcdiἾὁỸr;愯oô͒ĀahὉὋ;䎷耻ð䃰Āmrὓὗl耻ë䃫o;悬ƀcipὡὤὧl;䀡sôծĀeoὬὴctatioîՙnentialåչৡᾒ\0ᾞ\0ᾡᾧ\0\0ῆῌ\0ΐ\0ῦῪ \0 ⁚llingdotseñṄy;䑄male;晀ƀilrᾭᾳ῁lig;耀ﬃɩᾹ\0\0᾽g;耀ﬀig;耀ﬄ;쀀𝔣lig;耀ﬁlig;쀀fjƀaltῙ῜ῡt;晭ig;耀ﬂns;斱of;䆒ǰ΅\0ῳf;쀀𝕗ĀakֿῷĀ;vῼ´拔;櫙artint;樍Āao‌⁕Ācs‑⁒α‚‰‸⁅⁈\0⁐β•‥‧‪‬\0‮耻½䂽;慓耻¼䂼;慕;慙;慛Ƴ‴\0‶;慔;慖ʴ‾⁁\0\0⁃耻¾䂾;慗;慜5;慘ƶ⁌\0⁎;慚;慝8;慞l;恄wn;挢cr;쀀𝒻ࢀEabcdefgijlnorstv₂₉₟₥₰₴⃰⃵⃺⃿℃ℒℸ̗ℾ⅒↞Ā;lٍ₇;檌ƀcmpₐₕ₝ute;䇵maĀ;dₜ᳚䎳;檆reve;䄟Āiy₪₮rc;䄝;䐳ot;䄡Ȁ;lqsؾق₽⃉ƀ;qsؾٌ⃄lanô٥Ȁ;cdl٥⃒⃥⃕c;檩otĀ;o⃜⃝檀Ā;l⃢⃣檂;檄Ā;e⃪⃭쀀⋛︀s;檔r;쀀𝔤Ā;gٳ؛mel;愷cy;䑓Ȁ;Eajٚℌℎℐ;檒;檥;檤ȀEaesℛℝ℩ℴ;扩pĀ;p℣ℤ檊rox»ℤĀ;q℮ℯ檈Ā;q℮ℛim;拧pf;쀀𝕘Āci⅃ⅆr;愊mƀ;el٫ⅎ⅐;檎;檐茀>;cdlqr׮ⅠⅪⅮⅳⅹĀciⅥⅧ;檧r;橺ot;拗Par;榕uest;橼ʀadelsↄⅪ←ٖ↛ǰ↉\0↎proø₞r;楸qĀlqؿ↖lesó₈ií٫Āen↣↭rtneqq;쀀≩︀Å↪ԀAabcefkosy⇄⇇⇱⇵⇺∘∝∯≨≽ròΠȀilmr⇐⇔⇗⇛rsðᒄf»․ilôکĀdr⇠⇤cy;䑊ƀ;cwࣴ⇫⇯ir;楈;憭ar;意irc;䄥ƀalr∁∎∓rtsĀ;u∉∊晥it»∊lip;怦con;抹r;쀀𝔥sĀew∣∩arow;椥arow;椦ʀamopr∺∾≃≞≣rr;懿tht;戻kĀlr≉≓eftarrow;憩ightarrow;憪f;쀀𝕙bar;怕ƀclt≯≴≸r;쀀𝒽asè⇴rok;䄧Ābp⊂⊇ull;恃hen»ᱛૡ⊣\0⊪\0⊸⋅⋎\0⋕⋳\0\0⋸⌢⍧⍢⍿\0⎆⎪⎴cute耻í䃭ƀ;iyݱ⊰⊵rc耻î䃮;䐸Ācx⊼⊿y;䐵cl耻¡䂡ĀfrΟ⋉;쀀𝔦rave耻ì䃬Ȁ;inoܾ⋝⋩⋮Āin⋢⋦nt;樌t;戭fin;槜ta;愩lig;䄳ƀaop⋾⌚⌝ƀcgt⌅⌈⌗r;䄫ƀelpܟ⌏⌓inåގarôܠh;䄱f;抷ed;䆵ʀ;cfotӴ⌬⌱⌽⍁are;愅inĀ;t⌸⌹戞ie;槝doô⌙ʀ;celpݗ⍌⍐⍛⍡al;抺Āgr⍕⍙eróᕣã⍍arhk;樗rod;樼Ȁcgpt⍯⍲⍶⍻y;䑑on;䄯f;쀀𝕚a;䎹uest耻¿䂿Āci⎊⎏r;쀀𝒾nʀ;EdsvӴ⎛⎝⎡ӳ;拹ot;拵Ā;v⎦⎧拴;拳Ā;iݷ⎮lde;䄩ǫ⎸\0⎼cy;䑖l耻ï䃯̀cfmosu⏌⏗⏜⏡⏧⏵Āiy⏑⏕rc;䄵;䐹r;쀀𝔧ath;䈷pf;쀀𝕛ǣ⏬\0⏱r;쀀𝒿rcy;䑘kcy;䑔Ѐacfghjos␋␖␢␧␭␱␵␻ppaĀ;v␓␔䎺;䏰Āey␛␠dil;䄷;䐺r;쀀𝔨reen;䄸cy;䑅cy;䑜pf;쀀𝕜cr;쀀𝓀஀ABEHabcdefghjlmnoprstuv⑰⒁⒆⒍⒑┎┽╚▀♎♞♥♹♽⚚⚲⛘❝❨➋⟀⠁⠒ƀart⑷⑺⑼rò৆òΕail;椛arr;椎Ā;gঔ⒋;檋ar;楢ॣ⒥\0⒪\0⒱\0\0\0\0\0⒵Ⓔ\0ⓆⓈⓍ\0⓹ute;䄺mptyv;榴raîࡌbda;䎻gƀ;dlࢎⓁⓃ;榑åࢎ;檅uo耻«䂫rЀ;bfhlpst࢙ⓞⓦⓩ⓫⓮⓱⓵Ā;f࢝ⓣs;椟s;椝ë≒p;憫l;椹im;楳l;憢ƀ;ae⓿─┄檫il;椙Ā;s┉┊檭;쀀⪭︀ƀabr┕┙┝rr;椌rk;杲Āak┢┬cĀek┨┪;䁻;䁛Āes┱┳;榋lĀdu┹┻;榏;榍Ȁaeuy╆╋╖╘ron;䄾Ādi═╔il;䄼ìࢰâ┩;䐻Ȁcqrs╣╦╭╽a;椶uoĀ;rนᝆĀdu╲╷har;楧shar;楋h;憲ʀ;fgqs▋▌উ◳◿扤tʀahlrt▘▤▷◂◨rrowĀ;t࢙□aé⓶arpoonĀdu▯▴own»њp»०eftarrows;懇ightƀahs◍◖◞rrowĀ;sࣴࢧarpoonó྘quigarro÷⇰hreetimes;拋ƀ;qs▋ও◺lanôবʀ;cdgsব☊☍☝☨c;檨otĀ;o☔☕橿Ā;r☚☛檁;檃Ā;e☢☥쀀⋚︀s;檓ʀadegs☳☹☽♉♋pproøⓆot;拖qĀgq♃♅ôউgtò⒌ôছiíলƀilr♕࣡♚sht;楼;쀀𝔩Ā;Eজ♣;檑š♩♶rĀdu▲♮Ā;l॥♳;楪lk;斄cy;䑙ʀ;achtੈ⚈⚋⚑⚖rò◁orneòᴈard;楫ri;旺Āio⚟⚤dot;䅀ustĀ;a⚬⚭掰che»⚭ȀEaes⚻⚽⛉⛔;扨pĀ;p⛃⛄檉rox»⛄Ā;q⛎⛏檇Ā;q⛎⚻im;拦Ѐabnoptwz⛩⛴⛷✚✯❁❇❐Ānr⛮⛱g;柬r;懽rëࣁgƀlmr⛿✍✔eftĀar০✇ightá৲apsto;柼ightá৽parrowĀlr✥✩efô⓭ight;憬ƀafl✶✹✽r;榅;쀀𝕝us;樭imes;樴š❋❏st;戗áፎƀ;ef❗❘᠀旊nge»❘arĀ;l❤❥䀨t;榓ʀachmt❳❶❼➅➇ròࢨorneòᶌarĀ;d྘➃;業;怎ri;抿̀achiqt➘➝ੀ➢➮➻quo;怹r;쀀𝓁mƀ;egল➪➬;檍;檏Ābu┪➳oĀ;rฟ➹;怚rok;䅂萀<;cdhilqrࠫ⟒☹⟜⟠⟥⟪⟰Āci⟗⟙;檦r;橹reå◲mes;拉arr;楶uest;橻ĀPi⟵⟹ar;榖ƀ;ef⠀भ᠛旃rĀdu⠇⠍shar;楊har;楦Āen⠗⠡rtneqq;쀀≨︀Å⠞܀Dacdefhilnopsu⡀⡅⢂⢎⢓⢠⢥⢨⣚⣢⣤ઃ⣳⤂Dot;戺Ȁclpr⡎⡒⡣⡽r耻¯䂯Āet⡗⡙;時Ā;e⡞⡟朠se»⡟Ā;sျ⡨toȀ;dluျ⡳⡷⡻owîҌefôएðᏑker;斮Āoy⢇⢌mma;権;䐼ash;怔asuredangle»ᘦr;쀀𝔪o;愧ƀcdn⢯⢴⣉ro耻µ䂵Ȁ;acdᑤ⢽⣀⣄sôᚧir;櫰ot肻·Ƶusƀ;bd⣒ᤃ⣓戒Ā;uᴼ⣘;横ţ⣞⣡p;櫛ò−ðઁĀdp⣩⣮els;抧f;쀀𝕞Āct⣸⣽r;쀀𝓂pos»ᖝƀ;lm⤉⤊⤍䎼timap;抸ఀGLRVabcdefghijlmoprstuvw⥂⥓⥾⦉⦘⧚⧩⨕⨚⩘⩝⪃⪕⪤⪨⬄⬇⭄⭿⮮ⰴⱧⱼ⳩Āgt⥇⥋;쀀⋙̸Ā;v⥐௏쀀≫⃒ƀelt⥚⥲⥶ftĀar⥡⥧rrow;懍ightarrow;懎;쀀⋘̸Ā;v⥻ే쀀≪⃒ightarrow;懏ĀDd⦎⦓ash;抯ash;抮ʀbcnpt⦣⦧⦬⦱⧌la»˞ute;䅄g;쀀∠⃒ʀ;Eiop඄⦼⧀⧅⧈;쀀⩰̸d;쀀≋̸s;䅉roø඄urĀ;a⧓⧔普lĀ;s⧓ସǳ⧟\0⧣p肻\xA0ଷmpĀ;e௹ఀʀaeouy⧴⧾⨃⨐⨓ǰ⧹\0⧻;橃on;䅈dil;䅆ngĀ;dൾ⨊ot;쀀⩭̸p;橂;䐽ash;怓΀;Aadqsxஒ⨩⨭⨻⩁⩅⩐rr;懗rĀhr⨳⨶k;椤Ā;oᏲᏰot;쀀≐̸uiöୣĀei⩊⩎ar;椨í஘istĀ;s஠டr;쀀𝔫ȀEest௅⩦⩹⩼ƀ;qs஼⩭௡ƀ;qs஼௅⩴lanô௢ií௪Ā;rஶ⪁»ஷƀAap⪊⪍⪑rò⥱rr;憮ar;櫲ƀ;svྍ⪜ྌĀ;d⪡⪢拼;拺cy;䑚΀AEadest⪷⪺⪾⫂⫅⫶⫹rò⥦;쀀≦̸rr;憚r;急Ȁ;fqs఻⫎⫣⫯tĀar⫔⫙rro÷⫁ightarro÷⪐ƀ;qs఻⪺⫪lanôౕĀ;sౕ⫴»శiíౝĀ;rవ⫾iĀ;eచథiäඐĀpt⬌⬑f;쀀𝕟膀¬;in⬙⬚⬶䂬nȀ;Edvஉ⬤⬨⬮;쀀⋹̸ot;쀀⋵̸ǡஉ⬳⬵;拷;拶iĀ;vಸ⬼ǡಸ⭁⭃;拾;拽ƀaor⭋⭣⭩rȀ;ast୻⭕⭚⭟lleì୻l;쀀⫽⃥;쀀∂̸lint;樔ƀ;ceಒ⭰⭳uåಥĀ;cಘ⭸Ā;eಒ⭽ñಘȀAait⮈⮋⮝⮧rò⦈rrƀ;cw⮔⮕⮙憛;쀀⤳̸;쀀↝̸ghtarrow»⮕riĀ;eೋೖ΀chimpqu⮽⯍⯙⬄୸⯤⯯Ȁ;cerല⯆ഷ⯉uå൅;쀀𝓃ortɭ⬅\0\0⯖ará⭖mĀ;e൮⯟Ā;q൴൳suĀbp⯫⯭å೸åഋƀbcp⯶ⰑⰙȀ;Ees⯿ⰀഢⰄ抄;쀀⫅̸etĀ;eഛⰋqĀ;qണⰀcĀ;eലⰗñസȀ;EesⰢⰣൟⰧ抅;쀀⫆̸etĀ;e൘ⰮqĀ;qൠⰣȀgilrⰽⰿⱅⱇìௗlde耻ñ䃱çృiangleĀlrⱒⱜeftĀ;eచⱚñదightĀ;eೋⱥñ೗Ā;mⱬⱭ䎽ƀ;esⱴⱵⱹ䀣ro;愖p;怇ҀDHadgilrsⲏⲔⲙⲞⲣⲰⲶⳓⳣash;抭arr;椄p;쀀≍⃒ash;抬ĀetⲨⲬ;쀀≥⃒;쀀>⃒nfin;槞ƀAetⲽⳁⳅrr;椂;쀀≤⃒Ā;rⳊⳍ쀀<⃒ie;쀀⊴⃒ĀAtⳘⳜrr;椃rie;쀀⊵⃒im;쀀∼⃒ƀAan⳰⳴ⴂrr;懖rĀhr⳺⳽k;椣Ā;oᏧᏥear;椧ቓ᪕\0\0\0\0\0\0\0\0\0\0\0\0\0ⴭ\0ⴸⵈⵠⵥ⵲ⶄᬇ\0\0ⶍⶫ\0ⷈⷎ\0ⷜ⸙⸫⸾⹃Ācsⴱ᪗ute耻ó䃳ĀiyⴼⵅrĀ;c᪞ⵂ耻ô䃴;䐾ʀabios᪠ⵒⵗǈⵚlac;䅑v;樸old;榼lig;䅓Ācr⵩⵭ir;榿;쀀𝔬ͯ⵹\0\0⵼\0ⶂn;䋛ave耻ò䃲;槁Ābmⶈ෴ar;榵Ȁacitⶕ⶘ⶥⶨrò᪀Āir⶝ⶠr;榾oss;榻nå๒;槀ƀaeiⶱⶵⶹcr;䅍ga;䏉ƀcdnⷀⷅǍron;䎿;榶pf;쀀𝕠ƀaelⷔ⷗ǒr;榷rp;榹΀;adiosvⷪⷫⷮ⸈⸍⸐⸖戨rò᪆Ȁ;efmⷷⷸ⸂⸅橝rĀ;oⷾⷿ愴f»ⷿ耻ª䂪耻º䂺gof;抶r;橖lope;橗;橛ƀclo⸟⸡⸧ò⸁ash耻ø䃸l;折iŬⸯ⸴de耻õ䃵esĀ;aǛ⸺s;樶ml耻ö䃶bar;挽ૡ⹞\0⹽\0⺀⺝\0⺢⺹\0\0⻋ຜ\0⼓\0\0⼫⾼\0⿈rȀ;astЃ⹧⹲຅脀¶;l⹭⹮䂶leìЃɩ⹸\0\0⹻m;櫳;櫽y;䐿rʀcimpt⺋⺏⺓ᡥ⺗nt;䀥od;䀮il;怰enk;怱r;쀀𝔭ƀimo⺨⺰⺴Ā;v⺭⺮䏆;䏕maô੶ne;明ƀ;tv⺿⻀⻈䏀chfork»´;䏖Āau⻏⻟nĀck⻕⻝kĀ;h⇴⻛;愎ö⇴sҀ;abcdemst⻳⻴ᤈ⻹⻽⼄⼆⼊⼎䀫cir;樣ir;樢Āouᵀ⼂;樥;橲n肻±ຝim;樦wo;樧ƀipu⼙⼠⼥ntint;樕f;쀀𝕡nd耻£䂣Ԁ;Eaceinosu່⼿⽁⽄⽇⾁⾉⾒⽾⾶;檳p;檷uå໙Ā;c໎⽌̀;acens່⽙⽟⽦⽨⽾pproø⽃urlyeñ໙ñ໎ƀaes⽯⽶⽺pprox;檹qq;檵im;拨iíໟmeĀ;s⾈ຮ怲ƀEas⽸⾐⽺ð⽵ƀdfp໬⾙⾯ƀals⾠⾥⾪lar;挮ine;挒urf;挓Ā;t໻⾴ï໻rel;抰Āci⿀⿅r;쀀𝓅;䏈ncsp;怈̀fiopsu⿚⋢⿟⿥⿫⿱r;쀀𝔮pf;쀀𝕢rime;恗cr;쀀𝓆ƀaeo⿸〉〓tĀei⿾々rnionóڰnt;樖stĀ;e【】䀿ñἙô༔઀ABHabcdefhilmnoprstux぀けさすムㄎㄫㅇㅢㅲㆎ㈆㈕㈤㈩㉘㉮㉲㊐㊰㊷ƀartぇおがròႳòϝail;検aròᱥar;楤΀cdenqrtとふへみわゔヌĀeuねぱ;쀀∽̱te;䅕iãᅮmptyv;榳gȀ;del࿑らるろ;榒;榥å࿑uo耻»䂻rր;abcfhlpstw࿜ガクシスゼゾダッデナp;極Ā;f࿠ゴs;椠;椳s;椞ë≝ð✮l;楅im;楴l;憣;憝Āaiパフil;椚oĀ;nホボ戶aló༞ƀabrョリヮrò៥rk;杳ĀakンヽcĀekヹ・;䁽;䁝Āes㄂㄄;榌lĀduㄊㄌ;榎;榐Ȁaeuyㄗㄜㄧㄩron;䅙Ādiㄡㄥil;䅗ì࿲âヺ;䑀Ȁclqsㄴㄷㄽㅄa;椷dhar;楩uoĀ;rȎȍh;憳ƀacgㅎㅟངlȀ;ipsླྀㅘㅛႜnåႻarôྩt;断ƀilrㅩဣㅮsht;楽;쀀𝔯ĀaoㅷㆆrĀduㅽㅿ»ѻĀ;l႑ㆄ;楬Ā;vㆋㆌ䏁;䏱ƀgns㆕ㇹㇼht̀ahlrstㆤㆰ㇂㇘㇤㇮rrowĀ;t࿜ㆭaéトarpoonĀduㆻㆿowîㅾp»႒eftĀah㇊㇐rrowó࿪arpoonóՑightarrows;應quigarro÷ニhreetimes;拌g;䋚ingdotseñἲƀahm㈍㈐㈓rò࿪aòՑ;怏oustĀ;a㈞㈟掱che»㈟mid;櫮Ȁabpt㈲㈽㉀㉒Ānr㈷㈺g;柭r;懾rëဃƀafl㉇㉊㉎r;榆;쀀𝕣us;樮imes;樵Āap㉝㉧rĀ;g㉣㉤䀩t;榔olint;樒arò㇣Ȁachq㉻㊀Ⴜ㊅quo;怺r;쀀𝓇Ābu・㊊oĀ;rȔȓƀhir㊗㊛㊠reåㇸmes;拊iȀ;efl㊪ၙᠡ㊫方tri;槎luhar;楨;愞ൡ㋕㋛㋟㌬㌸㍱\0㍺㎤\0\0㏬㏰\0㐨㑈㑚㒭㒱㓊㓱\0㘖\0\0㘳cute;䅛quï➺Ԁ;Eaceinpsyᇭ㋳㋵㋿㌂㌋㌏㌟㌦㌩;檴ǰ㋺\0㋼;檸on;䅡uåᇾĀ;dᇳ㌇il;䅟rc;䅝ƀEas㌖㌘㌛;檶p;檺im;择olint;樓iíሄ;䑁otƀ;be㌴ᵇ㌵担;橦΀Aacmstx㍆㍊㍗㍛㍞㍣㍭rr;懘rĀhr㍐㍒ë∨Ā;oਸ਼਴t耻§䂧i;䀻war;椩mĀin㍩ðnuóñt;朶rĀ;o㍶⁕쀀𝔰Ȁacoy㎂㎆㎑㎠rp;景Āhy㎋㎏cy;䑉;䑈rtɭ㎙\0\0㎜iäᑤaraì⹯耻­䂭Āgm㎨㎴maƀ;fv㎱㎲㎲䏃;䏂Ѐ;deglnprካ㏅㏉㏎㏖㏞㏡㏦ot;橪Ā;q኱ኰĀ;E㏓㏔檞;檠Ā;E㏛㏜檝;檟e;扆lus;樤arr;楲aròᄽȀaeit㏸㐈㐏㐗Āls㏽㐄lsetmé㍪hp;樳parsl;槤Ādlᑣ㐔e;挣Ā;e㐜㐝檪Ā;s㐢㐣檬;쀀⪬︀ƀflp㐮㐳㑂tcy;䑌Ā;b㐸㐹䀯Ā;a㐾㐿槄r;挿f;쀀𝕤aĀdr㑍ЂesĀ;u㑔㑕晠it»㑕ƀcsu㑠㑹㒟Āau㑥㑯pĀ;sᆈ㑫;쀀⊓︀pĀ;sᆴ㑵;쀀⊔︀uĀbp㑿㒏ƀ;esᆗᆜ㒆etĀ;eᆗ㒍ñᆝƀ;esᆨᆭ㒖etĀ;eᆨ㒝ñᆮƀ;afᅻ㒦ְrť㒫ֱ»ᅼaròᅈȀcemt㒹㒾㓂㓅r;쀀𝓈tmîñiì㐕aræᆾĀar㓎㓕rĀ;f㓔ឿ昆Āan㓚㓭ightĀep㓣㓪psiloîỠhé⺯s»⡒ʀbcmnp㓻㕞ሉ㖋㖎Ҁ;Edemnprs㔎㔏㔑㔕㔞㔣㔬㔱㔶抂;櫅ot;檽Ā;dᇚ㔚ot;櫃ult;櫁ĀEe㔨㔪;櫋;把lus;檿arr;楹ƀeiu㔽㕒㕕tƀ;en㔎㕅㕋qĀ;qᇚ㔏eqĀ;q㔫㔨m;櫇Ābp㕚㕜;櫕;櫓c̀;acensᇭ㕬㕲㕹㕻㌦pproø㋺urlyeñᇾñᇳƀaes㖂㖈㌛pproø㌚qñ㌗g;晪ڀ123;Edehlmnps㖩㖬㖯ሜ㖲㖴㗀㗉㗕㗚㗟㗨㗭耻¹䂹耻²䂲耻³䂳;櫆Āos㖹㖼t;檾ub;櫘Ā;dሢ㗅ot;櫄sĀou㗏㗒l;柉b;櫗arr;楻ult;櫂ĀEe㗤㗦;櫌;抋lus;櫀ƀeiu㗴㘉㘌tƀ;enሜ㗼㘂qĀ;qሢ㖲eqĀ;q㗧㗤m;櫈Ābp㘑㘓;櫔;櫖ƀAan㘜㘠㘭rr;懙rĀhr㘦㘨ë∮Ā;oਫ਩war;椪lig耻ß䃟௡㙑㙝㙠ዎ㙳㙹\0㙾㛂\0\0\0\0\0㛛㜃\0㜉㝬\0\0\0㞇ɲ㙖\0\0㙛get;挖;䏄rë๟ƀaey㙦㙫㙰ron;䅥dil;䅣;䑂lrec;挕r;쀀𝔱Ȁeiko㚆㚝㚵㚼ǲ㚋\0㚑eĀ4fኄኁaƀ;sv㚘㚙㚛䎸ym;䏑Ācn㚢㚲kĀas㚨㚮pproø዁im»ኬsðኞĀas㚺㚮ð዁rn耻þ䃾Ǭ̟㛆⋧es膀×;bd㛏㛐㛘䃗Ā;aᤏ㛕r;樱;樰ƀeps㛡㛣㜀á⩍Ȁ;bcf҆㛬㛰㛴ot;挶ir;櫱Ā;o㛹㛼쀀𝕥rk;櫚á㍢rime;怴ƀaip㜏㜒㝤dåቈ΀adempst㜡㝍㝀㝑㝗㝜㝟ngleʀ;dlqr㜰㜱㜶㝀㝂斵own»ᶻeftĀ;e⠀㜾ñम;扜ightĀ;e㊪㝋ñၚot;旬inus;樺lus;樹b;槍ime;樻ezium;揢ƀcht㝲㝽㞁Āry㝷㝻;쀀𝓉;䑆cy;䑛rok;䅧Āio㞋㞎xô᝷headĀlr㞗㞠eftarro÷ࡏightarrow»ཝऀAHabcdfghlmoprstuw㟐㟓㟗㟤㟰㟼㠎㠜㠣㠴㡑㡝㡫㢩㣌㣒㣪㣶ròϭar;楣Ācr㟜㟢ute耻ú䃺òᅐrǣ㟪\0㟭y;䑞ve;䅭Āiy㟵㟺rc耻û䃻;䑃ƀabh㠃㠆㠋ròᎭlac;䅱aòᏃĀir㠓㠘sht;楾;쀀𝔲rave耻ù䃹š㠧㠱rĀlr㠬㠮»ॗ»ႃlk;斀Āct㠹㡍ɯ㠿\0\0㡊rnĀ;e㡅㡆挜r»㡆op;挏ri;旸Āal㡖㡚cr;䅫肻¨͉Āgp㡢㡦on;䅳f;쀀𝕦̀adhlsuᅋ㡸㡽፲㢑㢠ownáᎳarpoonĀlr㢈㢌efô㠭ighô㠯iƀ;hl㢙㢚㢜䏅»ᏺon»㢚parrows;懈ƀcit㢰㣄㣈ɯ㢶\0\0㣁rnĀ;e㢼㢽挝r»㢽op;挎ng;䅯ri;旹cr;쀀𝓊ƀdir㣙㣝㣢ot;拰lde;䅩iĀ;f㜰㣨»᠓Āam㣯㣲rò㢨l耻ü䃼angle;榧ހABDacdeflnoprsz㤜㤟㤩㤭㦵㦸㦽㧟㧤㧨㧳㧹㧽㨁㨠ròϷarĀ;v㤦㤧櫨;櫩asèϡĀnr㤲㤷grt;榜΀eknprst㓣㥆㥋㥒㥝㥤㦖appá␕othinçẖƀhir㓫⻈㥙opô⾵Ā;hᎷ㥢ïㆍĀiu㥩㥭gmá㎳Ābp㥲㦄setneqĀ;q㥽㦀쀀⊊︀;쀀⫋︀setneqĀ;q㦏㦒쀀⊋︀;쀀⫌︀Āhr㦛㦟etá㚜iangleĀlr㦪㦯eft»थight»ၑy;䐲ash»ံƀelr㧄㧒㧗ƀ;beⷪ㧋㧏ar;抻q;扚lip;拮Ābt㧜ᑨaòᑩr;쀀𝔳tré㦮suĀbp㧯㧱»ജ»൙pf;쀀𝕧roð໻tré㦴Ācu㨆㨋r;쀀𝓋Ābp㨐㨘nĀEe㦀㨖»㥾nĀEe㦒㨞»㦐igzag;榚΀cefoprs㨶㨻㩖㩛㩔㩡㩪irc;䅵Ādi㩀㩑Ābg㩅㩉ar;機eĀ;qᗺ㩏;扙erp;愘r;쀀𝔴pf;쀀𝕨Ā;eᑹ㩦atèᑹcr;쀀𝓌ૣណ㪇\0㪋\0㪐㪛\0\0㪝㪨㪫㪯\0\0㫃㫎\0㫘ៜ៟tré៑r;쀀𝔵ĀAa㪔㪗ròσrò৶;䎾ĀAa㪡㪤ròθrò৫að✓is;拻ƀdptឤ㪵㪾Āfl㪺ឩ;쀀𝕩imåឲĀAa㫇㫊ròώròਁĀcq㫒ីr;쀀𝓍Āpt៖㫜ré។Ѐacefiosu㫰㫽㬈㬌㬑㬕㬛㬡cĀuy㫶㫻te耻ý䃽;䑏Āiy㬂㬆rc;䅷;䑋n耻¥䂥r;쀀𝔶cy;䑗pf;쀀𝕪cr;쀀𝓎Ācm㬦㬩y;䑎l耻ÿ䃿Ԁacdefhiosw㭂㭈㭔㭘㭤㭩㭭㭴㭺㮀cute;䅺Āay㭍㭒ron;䅾;䐷ot;䅼Āet㭝㭡træᕟa;䎶r;쀀𝔷cy;䐶grarr;懝pf;쀀𝕫cr;쀀𝓏Ājn㮅㮇;怍j;怌`.split(``).map(function(e) {
		return e.charCodeAt(0);
	}));
})), l = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.default = new Uint16Array(`Ȁaglq	\x1Bɭ\0\0p;䀦os;䀧t;䀾t;䀼uot;䀢`.split(``).map(function(e) {
		return e.charCodeAt(0);
	}));
})), u = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.replaceCodePoint = e.fromCodePoint = void 0;
	var t = /* @__PURE__ */ new Map([
		[0, 65533],
		[128, 8364],
		[130, 8218],
		[131, 402],
		[132, 8222],
		[133, 8230],
		[134, 8224],
		[135, 8225],
		[136, 710],
		[137, 8240],
		[138, 352],
		[139, 8249],
		[140, 338],
		[142, 381],
		[145, 8216],
		[146, 8217],
		[147, 8220],
		[148, 8221],
		[149, 8226],
		[150, 8211],
		[151, 8212],
		[152, 732],
		[153, 8482],
		[154, 353],
		[155, 8250],
		[156, 339],
		[158, 382],
		[159, 376]
	]);
	e.fromCodePoint = String.fromCodePoint ?? function(e) {
		var t = ``;
		return e > 65535 && (e -= 65536, t += String.fromCharCode(e >>> 10 & 1023 | 55296), e = 56320 | e & 1023), t += String.fromCharCode(e), t;
	};
	function n(e) {
		return e >= 55296 && e <= 57343 || e > 1114111 ? 65533 : t.get(e) ?? e;
	}
	e.replaceCodePoint = n;
	function r(t) {
		return (0, e.fromCodePoint)(n(t));
	}
	e.default = r;
})), d = e(((e) => {
	var t = e && e.__createBinding || (Object.create ? (function(e, t, n, r) {
		r === void 0 && (r = n);
		var i = Object.getOwnPropertyDescriptor(t, n);
		(!i || (`get` in i ? !t.__esModule : i.writable || i.configurable)) && (i = {
			enumerable: !0,
			get: function() {
				return t[n];
			}
		}), Object.defineProperty(e, r, i);
	}) : (function(e, t, n, r) {
		r === void 0 && (r = n), e[r] = t[n];
	})), n = e && e.__setModuleDefault || (Object.create ? (function(e, t) {
		Object.defineProperty(e, "default", {
			enumerable: !0,
			value: t
		});
	}) : function(e, t) {
		e.default = t;
	}), r = e && e.__importStar || function(e) {
		if (e && e.__esModule) return e;
		var r = {};
		if (e != null) for (var i in e) i !== "default" && Object.prototype.hasOwnProperty.call(e, i) && t(r, e, i);
		return n(r, e), r;
	}, i = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.decodeXML = e.decodeHTMLStrict = e.decodeHTMLAttribute = e.decodeHTML = e.determineBranch = e.EntityDecoder = e.DecodingMode = e.BinTrieFlags = e.fromCodePoint = e.replaceCodePoint = e.decodeCodePoint = e.xmlDecodeTree = e.htmlDecodeTree = void 0;
	var a = i(c());
	e.htmlDecodeTree = a.default;
	var o = i(l());
	e.xmlDecodeTree = o.default;
	var s = r(u());
	e.decodeCodePoint = s.default;
	var d = u();
	Object.defineProperty(e, "replaceCodePoint", {
		enumerable: !0,
		get: function() {
			return d.replaceCodePoint;
		}
	}), Object.defineProperty(e, "fromCodePoint", {
		enumerable: !0,
		get: function() {
			return d.fromCodePoint;
		}
	});
	var f;
	(function(e) {
		e[e.NUM = 35] = `NUM`, e[e.SEMI = 59] = `SEMI`, e[e.EQUALS = 61] = `EQUALS`, e[e.ZERO = 48] = `ZERO`, e[e.NINE = 57] = `NINE`, e[e.LOWER_A = 97] = `LOWER_A`, e[e.LOWER_F = 102] = `LOWER_F`, e[e.LOWER_X = 120] = `LOWER_X`, e[e.LOWER_Z = 122] = `LOWER_Z`, e[e.UPPER_A = 65] = `UPPER_A`, e[e.UPPER_F = 70] = `UPPER_F`, e[e.UPPER_Z = 90] = `UPPER_Z`;
	})(f ||= {});
	var p = 32, m;
	(function(e) {
		e[e.VALUE_LENGTH = 49152] = `VALUE_LENGTH`, e[e.BRANCH_LENGTH = 16256] = `BRANCH_LENGTH`, e[e.JUMP_TABLE = 127] = `JUMP_TABLE`;
	})(m = e.BinTrieFlags ||= {});
	function h(e) {
		return e >= f.ZERO && e <= f.NINE;
	}
	function g(e) {
		return e >= f.UPPER_A && e <= f.UPPER_F || e >= f.LOWER_A && e <= f.LOWER_F;
	}
	function _(e) {
		return e >= f.UPPER_A && e <= f.UPPER_Z || e >= f.LOWER_A && e <= f.LOWER_Z || h(e);
	}
	function v(e) {
		return e === f.EQUALS || _(e);
	}
	var y;
	(function(e) {
		e[e.EntityStart = 0] = `EntityStart`, e[e.NumericStart = 1] = `NumericStart`, e[e.NumericDecimal = 2] = `NumericDecimal`, e[e.NumericHex = 3] = `NumericHex`, e[e.NamedEntity = 4] = `NamedEntity`;
	})(y ||= {});
	var b;
	(function(e) {
		e[e.Legacy = 0] = `Legacy`, e[e.Strict = 1] = `Strict`, e[e.Attribute = 2] = `Attribute`;
	})(b = e.DecodingMode ||= {});
	var x = function() {
		function e(e, t, n) {
			this.decodeTree = e, this.emitCodePoint = t, this.errors = n, this.state = y.EntityStart, this.consumed = 1, this.result = 0, this.treeIndex = 0, this.excess = 1, this.decodeMode = b.Strict;
		}
		return e.prototype.startEntity = function(e) {
			this.decodeMode = e, this.state = y.EntityStart, this.result = 0, this.treeIndex = 0, this.excess = 1, this.consumed = 1;
		}, e.prototype.write = function(e, t) {
			switch (this.state) {
				case y.EntityStart: return e.charCodeAt(t) === f.NUM ? (this.state = y.NumericStart, this.consumed += 1, this.stateNumericStart(e, t + 1)) : (this.state = y.NamedEntity, this.stateNamedEntity(e, t));
				case y.NumericStart: return this.stateNumericStart(e, t);
				case y.NumericDecimal: return this.stateNumericDecimal(e, t);
				case y.NumericHex: return this.stateNumericHex(e, t);
				case y.NamedEntity: return this.stateNamedEntity(e, t);
			}
		}, e.prototype.stateNumericStart = function(e, t) {
			return t >= e.length ? -1 : (e.charCodeAt(t) | p) === f.LOWER_X ? (this.state = y.NumericHex, this.consumed += 1, this.stateNumericHex(e, t + 1)) : (this.state = y.NumericDecimal, this.stateNumericDecimal(e, t));
		}, e.prototype.addToNumericResult = function(e, t, n, r) {
			if (t !== n) {
				var i = n - t;
				this.result = this.result * r ** +i + parseInt(e.substr(t, i), r), this.consumed += i;
			}
		}, e.prototype.stateNumericHex = function(e, t) {
			for (var n = t; t < e.length;) {
				var r = e.charCodeAt(t);
				if (h(r) || g(r)) t += 1;
				else return this.addToNumericResult(e, n, t, 16), this.emitNumericEntity(r, 3);
			}
			return this.addToNumericResult(e, n, t, 16), -1;
		}, e.prototype.stateNumericDecimal = function(e, t) {
			for (var n = t; t < e.length;) {
				var r = e.charCodeAt(t);
				if (h(r)) t += 1;
				else return this.addToNumericResult(e, n, t, 10), this.emitNumericEntity(r, 2);
			}
			return this.addToNumericResult(e, n, t, 10), -1;
		}, e.prototype.emitNumericEntity = function(e, t) {
			var n;
			if (this.consumed <= t) return (n = this.errors) == null || n.absenceOfDigitsInNumericCharacterReference(this.consumed), 0;
			if (e === f.SEMI) this.consumed += 1;
			else if (this.decodeMode === b.Strict) return 0;
			return this.emitCodePoint((0, s.replaceCodePoint)(this.result), this.consumed), this.errors && (e !== f.SEMI && this.errors.missingSemicolonAfterCharacterReference(), this.errors.validateNumericCharacterReference(this.result)), this.consumed;
		}, e.prototype.stateNamedEntity = function(e, t) {
			for (var n = this.decodeTree, r = n[this.treeIndex], i = (r & m.VALUE_LENGTH) >> 14; t < e.length; t++, this.excess++) {
				var a = e.charCodeAt(t);
				if (this.treeIndex = C(n, r, this.treeIndex + Math.max(1, i), a), this.treeIndex < 0) return this.result === 0 || this.decodeMode === b.Attribute && (i === 0 || v(a)) ? 0 : this.emitNotTerminatedNamedEntity();
				if (r = n[this.treeIndex], i = (r & m.VALUE_LENGTH) >> 14, i !== 0) {
					if (a === f.SEMI) return this.emitNamedEntityData(this.treeIndex, i, this.consumed + this.excess);
					this.decodeMode !== b.Strict && (this.result = this.treeIndex, this.consumed += this.excess, this.excess = 0);
				}
			}
			return -1;
		}, e.prototype.emitNotTerminatedNamedEntity = function() {
			var e, t = this, n = t.result, r = (t.decodeTree[n] & m.VALUE_LENGTH) >> 14;
			return this.emitNamedEntityData(n, r, this.consumed), (e = this.errors) == null || e.missingSemicolonAfterCharacterReference(), this.consumed;
		}, e.prototype.emitNamedEntityData = function(e, t, n) {
			var r = this.decodeTree;
			return this.emitCodePoint(t === 1 ? r[e] & ~m.VALUE_LENGTH : r[e + 1], n), t === 3 && this.emitCodePoint(r[e + 2], n), n;
		}, e.prototype.end = function() {
			var e;
			switch (this.state) {
				case y.NamedEntity: return this.result !== 0 && (this.decodeMode !== b.Attribute || this.result === this.treeIndex) ? this.emitNotTerminatedNamedEntity() : 0;
				case y.NumericDecimal: return this.emitNumericEntity(0, 2);
				case y.NumericHex: return this.emitNumericEntity(0, 3);
				case y.NumericStart: return (e = this.errors) == null || e.absenceOfDigitsInNumericCharacterReference(this.consumed), 0;
				case y.EntityStart: return 0;
			}
		}, e;
	}();
	e.EntityDecoder = x;
	function S(e) {
		var t = ``, n = new x(e, function(e) {
			return t += (0, s.fromCodePoint)(e);
		});
		return function(e, r) {
			for (var i = 0, a = 0; (a = e.indexOf(`&`, a)) >= 0;) {
				t += e.slice(i, a), n.startEntity(r);
				var o = n.write(e, a + 1);
				if (o < 0) {
					i = a + n.end();
					break;
				}
				i = a + o, a = o === 0 ? i + 1 : i;
			}
			var s = t + e.slice(i);
			return t = ``, s;
		};
	}
	function C(e, t, n, r) {
		var i = (t & m.BRANCH_LENGTH) >> 7, a = t & m.JUMP_TABLE;
		if (i === 0) return a !== 0 && r === a ? n : -1;
		if (a) {
			var o = r - a;
			return o < 0 || o >= i ? -1 : e[n + o] - 1;
		}
		for (var s = n, c = s + i - 1; s <= c;) {
			var l = s + c >>> 1, u = e[l];
			if (u < r) s = l + 1;
			else if (u > r) c = l - 1;
			else return e[l + i];
		}
		return -1;
	}
	e.determineBranch = C;
	var w = S(a.default), T = S(o.default);
	function E(e, t) {
		return t === void 0 && (t = b.Legacy), w(e, t);
	}
	e.decodeHTML = E;
	function D(e) {
		return w(e, b.Attribute);
	}
	e.decodeHTMLAttribute = D;
	function O(e) {
		return w(e, b.Strict);
	}
	e.decodeHTMLStrict = O;
	function k(e) {
		return T(e, b.Strict);
	}
	e.decodeXML = k;
})), f = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 });
	function t(e) {
		for (var t = 1; t < e.length; t++) e[t][0] += e[t - 1][0] + 1;
		return e;
	}
	e.default = new Map(t([
		[9, `&Tab;`],
		[0, `&NewLine;`],
		[22, `&excl;`],
		[0, `&quot;`],
		[0, `&num;`],
		[0, `&dollar;`],
		[0, `&percnt;`],
		[0, `&amp;`],
		[0, `&apos;`],
		[0, `&lpar;`],
		[0, `&rpar;`],
		[0, `&ast;`],
		[0, `&plus;`],
		[0, `&comma;`],
		[1, `&period;`],
		[0, `&sol;`],
		[10, `&colon;`],
		[0, `&semi;`],
		[0, {
			v: `&lt;`,
			n: 8402,
			o: `&nvlt;`
		}],
		[0, {
			v: `&equals;`,
			n: 8421,
			o: `&bne;`
		}],
		[0, {
			v: `&gt;`,
			n: 8402,
			o: `&nvgt;`
		}],
		[0, `&quest;`],
		[0, `&commat;`],
		[26, `&lbrack;`],
		[0, `&bsol;`],
		[0, `&rbrack;`],
		[0, `&Hat;`],
		[0, `&lowbar;`],
		[0, `&DiacriticalGrave;`],
		[5, {
			n: 106,
			o: `&fjlig;`
		}],
		[20, `&lbrace;`],
		[0, `&verbar;`],
		[0, `&rbrace;`],
		[34, `&nbsp;`],
		[0, `&iexcl;`],
		[0, `&cent;`],
		[0, `&pound;`],
		[0, `&curren;`],
		[0, `&yen;`],
		[0, `&brvbar;`],
		[0, `&sect;`],
		[0, `&die;`],
		[0, `&copy;`],
		[0, `&ordf;`],
		[0, `&laquo;`],
		[0, `&not;`],
		[0, `&shy;`],
		[0, `&circledR;`],
		[0, `&macr;`],
		[0, `&deg;`],
		[0, `&PlusMinus;`],
		[0, `&sup2;`],
		[0, `&sup3;`],
		[0, `&acute;`],
		[0, `&micro;`],
		[0, `&para;`],
		[0, `&centerdot;`],
		[0, `&cedil;`],
		[0, `&sup1;`],
		[0, `&ordm;`],
		[0, `&raquo;`],
		[0, `&frac14;`],
		[0, `&frac12;`],
		[0, `&frac34;`],
		[0, `&iquest;`],
		[0, `&Agrave;`],
		[0, `&Aacute;`],
		[0, `&Acirc;`],
		[0, `&Atilde;`],
		[0, `&Auml;`],
		[0, `&angst;`],
		[0, `&AElig;`],
		[0, `&Ccedil;`],
		[0, `&Egrave;`],
		[0, `&Eacute;`],
		[0, `&Ecirc;`],
		[0, `&Euml;`],
		[0, `&Igrave;`],
		[0, `&Iacute;`],
		[0, `&Icirc;`],
		[0, `&Iuml;`],
		[0, `&ETH;`],
		[0, `&Ntilde;`],
		[0, `&Ograve;`],
		[0, `&Oacute;`],
		[0, `&Ocirc;`],
		[0, `&Otilde;`],
		[0, `&Ouml;`],
		[0, `&times;`],
		[0, `&Oslash;`],
		[0, `&Ugrave;`],
		[0, `&Uacute;`],
		[0, `&Ucirc;`],
		[0, `&Uuml;`],
		[0, `&Yacute;`],
		[0, `&THORN;`],
		[0, `&szlig;`],
		[0, `&agrave;`],
		[0, `&aacute;`],
		[0, `&acirc;`],
		[0, `&atilde;`],
		[0, `&auml;`],
		[0, `&aring;`],
		[0, `&aelig;`],
		[0, `&ccedil;`],
		[0, `&egrave;`],
		[0, `&eacute;`],
		[0, `&ecirc;`],
		[0, `&euml;`],
		[0, `&igrave;`],
		[0, `&iacute;`],
		[0, `&icirc;`],
		[0, `&iuml;`],
		[0, `&eth;`],
		[0, `&ntilde;`],
		[0, `&ograve;`],
		[0, `&oacute;`],
		[0, `&ocirc;`],
		[0, `&otilde;`],
		[0, `&ouml;`],
		[0, `&div;`],
		[0, `&oslash;`],
		[0, `&ugrave;`],
		[0, `&uacute;`],
		[0, `&ucirc;`],
		[0, `&uuml;`],
		[0, `&yacute;`],
		[0, `&thorn;`],
		[0, `&yuml;`],
		[0, `&Amacr;`],
		[0, `&amacr;`],
		[0, `&Abreve;`],
		[0, `&abreve;`],
		[0, `&Aogon;`],
		[0, `&aogon;`],
		[0, `&Cacute;`],
		[0, `&cacute;`],
		[0, `&Ccirc;`],
		[0, `&ccirc;`],
		[0, `&Cdot;`],
		[0, `&cdot;`],
		[0, `&Ccaron;`],
		[0, `&ccaron;`],
		[0, `&Dcaron;`],
		[0, `&dcaron;`],
		[0, `&Dstrok;`],
		[0, `&dstrok;`],
		[0, `&Emacr;`],
		[0, `&emacr;`],
		[2, `&Edot;`],
		[0, `&edot;`],
		[0, `&Eogon;`],
		[0, `&eogon;`],
		[0, `&Ecaron;`],
		[0, `&ecaron;`],
		[0, `&Gcirc;`],
		[0, `&gcirc;`],
		[0, `&Gbreve;`],
		[0, `&gbreve;`],
		[0, `&Gdot;`],
		[0, `&gdot;`],
		[0, `&Gcedil;`],
		[1, `&Hcirc;`],
		[0, `&hcirc;`],
		[0, `&Hstrok;`],
		[0, `&hstrok;`],
		[0, `&Itilde;`],
		[0, `&itilde;`],
		[0, `&Imacr;`],
		[0, `&imacr;`],
		[2, `&Iogon;`],
		[0, `&iogon;`],
		[0, `&Idot;`],
		[0, `&imath;`],
		[0, `&IJlig;`],
		[0, `&ijlig;`],
		[0, `&Jcirc;`],
		[0, `&jcirc;`],
		[0, `&Kcedil;`],
		[0, `&kcedil;`],
		[0, `&kgreen;`],
		[0, `&Lacute;`],
		[0, `&lacute;`],
		[0, `&Lcedil;`],
		[0, `&lcedil;`],
		[0, `&Lcaron;`],
		[0, `&lcaron;`],
		[0, `&Lmidot;`],
		[0, `&lmidot;`],
		[0, `&Lstrok;`],
		[0, `&lstrok;`],
		[0, `&Nacute;`],
		[0, `&nacute;`],
		[0, `&Ncedil;`],
		[0, `&ncedil;`],
		[0, `&Ncaron;`],
		[0, `&ncaron;`],
		[0, `&napos;`],
		[0, `&ENG;`],
		[0, `&eng;`],
		[0, `&Omacr;`],
		[0, `&omacr;`],
		[2, `&Odblac;`],
		[0, `&odblac;`],
		[0, `&OElig;`],
		[0, `&oelig;`],
		[0, `&Racute;`],
		[0, `&racute;`],
		[0, `&Rcedil;`],
		[0, `&rcedil;`],
		[0, `&Rcaron;`],
		[0, `&rcaron;`],
		[0, `&Sacute;`],
		[0, `&sacute;`],
		[0, `&Scirc;`],
		[0, `&scirc;`],
		[0, `&Scedil;`],
		[0, `&scedil;`],
		[0, `&Scaron;`],
		[0, `&scaron;`],
		[0, `&Tcedil;`],
		[0, `&tcedil;`],
		[0, `&Tcaron;`],
		[0, `&tcaron;`],
		[0, `&Tstrok;`],
		[0, `&tstrok;`],
		[0, `&Utilde;`],
		[0, `&utilde;`],
		[0, `&Umacr;`],
		[0, `&umacr;`],
		[0, `&Ubreve;`],
		[0, `&ubreve;`],
		[0, `&Uring;`],
		[0, `&uring;`],
		[0, `&Udblac;`],
		[0, `&udblac;`],
		[0, `&Uogon;`],
		[0, `&uogon;`],
		[0, `&Wcirc;`],
		[0, `&wcirc;`],
		[0, `&Ycirc;`],
		[0, `&ycirc;`],
		[0, `&Yuml;`],
		[0, `&Zacute;`],
		[0, `&zacute;`],
		[0, `&Zdot;`],
		[0, `&zdot;`],
		[0, `&Zcaron;`],
		[0, `&zcaron;`],
		[19, `&fnof;`],
		[34, `&imped;`],
		[63, `&gacute;`],
		[65, `&jmath;`],
		[142, `&circ;`],
		[0, `&caron;`],
		[16, `&breve;`],
		[0, `&DiacriticalDot;`],
		[0, `&ring;`],
		[0, `&ogon;`],
		[0, `&DiacriticalTilde;`],
		[0, `&dblac;`],
		[51, `&DownBreve;`],
		[127, `&Alpha;`],
		[0, `&Beta;`],
		[0, `&Gamma;`],
		[0, `&Delta;`],
		[0, `&Epsilon;`],
		[0, `&Zeta;`],
		[0, `&Eta;`],
		[0, `&Theta;`],
		[0, `&Iota;`],
		[0, `&Kappa;`],
		[0, `&Lambda;`],
		[0, `&Mu;`],
		[0, `&Nu;`],
		[0, `&Xi;`],
		[0, `&Omicron;`],
		[0, `&Pi;`],
		[0, `&Rho;`],
		[1, `&Sigma;`],
		[0, `&Tau;`],
		[0, `&Upsilon;`],
		[0, `&Phi;`],
		[0, `&Chi;`],
		[0, `&Psi;`],
		[0, `&ohm;`],
		[7, `&alpha;`],
		[0, `&beta;`],
		[0, `&gamma;`],
		[0, `&delta;`],
		[0, `&epsi;`],
		[0, `&zeta;`],
		[0, `&eta;`],
		[0, `&theta;`],
		[0, `&iota;`],
		[0, `&kappa;`],
		[0, `&lambda;`],
		[0, `&mu;`],
		[0, `&nu;`],
		[0, `&xi;`],
		[0, `&omicron;`],
		[0, `&pi;`],
		[0, `&rho;`],
		[0, `&sigmaf;`],
		[0, `&sigma;`],
		[0, `&tau;`],
		[0, `&upsi;`],
		[0, `&phi;`],
		[0, `&chi;`],
		[0, `&psi;`],
		[0, `&omega;`],
		[7, `&thetasym;`],
		[0, `&Upsi;`],
		[2, `&phiv;`],
		[0, `&piv;`],
		[5, `&Gammad;`],
		[0, `&digamma;`],
		[18, `&kappav;`],
		[0, `&rhov;`],
		[3, `&epsiv;`],
		[0, `&backepsilon;`],
		[10, `&IOcy;`],
		[0, `&DJcy;`],
		[0, `&GJcy;`],
		[0, `&Jukcy;`],
		[0, `&DScy;`],
		[0, `&Iukcy;`],
		[0, `&YIcy;`],
		[0, `&Jsercy;`],
		[0, `&LJcy;`],
		[0, `&NJcy;`],
		[0, `&TSHcy;`],
		[0, `&KJcy;`],
		[1, `&Ubrcy;`],
		[0, `&DZcy;`],
		[0, `&Acy;`],
		[0, `&Bcy;`],
		[0, `&Vcy;`],
		[0, `&Gcy;`],
		[0, `&Dcy;`],
		[0, `&IEcy;`],
		[0, `&ZHcy;`],
		[0, `&Zcy;`],
		[0, `&Icy;`],
		[0, `&Jcy;`],
		[0, `&Kcy;`],
		[0, `&Lcy;`],
		[0, `&Mcy;`],
		[0, `&Ncy;`],
		[0, `&Ocy;`],
		[0, `&Pcy;`],
		[0, `&Rcy;`],
		[0, `&Scy;`],
		[0, `&Tcy;`],
		[0, `&Ucy;`],
		[0, `&Fcy;`],
		[0, `&KHcy;`],
		[0, `&TScy;`],
		[0, `&CHcy;`],
		[0, `&SHcy;`],
		[0, `&SHCHcy;`],
		[0, `&HARDcy;`],
		[0, `&Ycy;`],
		[0, `&SOFTcy;`],
		[0, `&Ecy;`],
		[0, `&YUcy;`],
		[0, `&YAcy;`],
		[0, `&acy;`],
		[0, `&bcy;`],
		[0, `&vcy;`],
		[0, `&gcy;`],
		[0, `&dcy;`],
		[0, `&iecy;`],
		[0, `&zhcy;`],
		[0, `&zcy;`],
		[0, `&icy;`],
		[0, `&jcy;`],
		[0, `&kcy;`],
		[0, `&lcy;`],
		[0, `&mcy;`],
		[0, `&ncy;`],
		[0, `&ocy;`],
		[0, `&pcy;`],
		[0, `&rcy;`],
		[0, `&scy;`],
		[0, `&tcy;`],
		[0, `&ucy;`],
		[0, `&fcy;`],
		[0, `&khcy;`],
		[0, `&tscy;`],
		[0, `&chcy;`],
		[0, `&shcy;`],
		[0, `&shchcy;`],
		[0, `&hardcy;`],
		[0, `&ycy;`],
		[0, `&softcy;`],
		[0, `&ecy;`],
		[0, `&yucy;`],
		[0, `&yacy;`],
		[1, `&iocy;`],
		[0, `&djcy;`],
		[0, `&gjcy;`],
		[0, `&jukcy;`],
		[0, `&dscy;`],
		[0, `&iukcy;`],
		[0, `&yicy;`],
		[0, `&jsercy;`],
		[0, `&ljcy;`],
		[0, `&njcy;`],
		[0, `&tshcy;`],
		[0, `&kjcy;`],
		[1, `&ubrcy;`],
		[0, `&dzcy;`],
		[7074, `&ensp;`],
		[0, `&emsp;`],
		[0, `&emsp13;`],
		[0, `&emsp14;`],
		[1, `&numsp;`],
		[0, `&puncsp;`],
		[0, `&ThinSpace;`],
		[0, `&hairsp;`],
		[0, `&NegativeMediumSpace;`],
		[0, `&zwnj;`],
		[0, `&zwj;`],
		[0, `&lrm;`],
		[0, `&rlm;`],
		[0, `&dash;`],
		[2, `&ndash;`],
		[0, `&mdash;`],
		[0, `&horbar;`],
		[0, `&Verbar;`],
		[1, `&lsquo;`],
		[0, `&CloseCurlyQuote;`],
		[0, `&lsquor;`],
		[1, `&ldquo;`],
		[0, `&CloseCurlyDoubleQuote;`],
		[0, `&bdquo;`],
		[1, `&dagger;`],
		[0, `&Dagger;`],
		[0, `&bull;`],
		[2, `&nldr;`],
		[0, `&hellip;`],
		[9, `&permil;`],
		[0, `&pertenk;`],
		[0, `&prime;`],
		[0, `&Prime;`],
		[0, `&tprime;`],
		[0, `&backprime;`],
		[3, `&lsaquo;`],
		[0, `&rsaquo;`],
		[3, `&oline;`],
		[2, `&caret;`],
		[1, `&hybull;`],
		[0, `&frasl;`],
		[10, `&bsemi;`],
		[7, `&qprime;`],
		[7, {
			v: `&MediumSpace;`,
			n: 8202,
			o: `&ThickSpace;`
		}],
		[0, `&NoBreak;`],
		[0, `&af;`],
		[0, `&InvisibleTimes;`],
		[0, `&ic;`],
		[72, `&euro;`],
		[46, `&tdot;`],
		[0, `&DotDot;`],
		[37, `&complexes;`],
		[2, `&incare;`],
		[4, `&gscr;`],
		[0, `&hamilt;`],
		[0, `&Hfr;`],
		[0, `&Hopf;`],
		[0, `&planckh;`],
		[0, `&hbar;`],
		[0, `&imagline;`],
		[0, `&Ifr;`],
		[0, `&lagran;`],
		[0, `&ell;`],
		[1, `&naturals;`],
		[0, `&numero;`],
		[0, `&copysr;`],
		[0, `&weierp;`],
		[0, `&Popf;`],
		[0, `&Qopf;`],
		[0, `&realine;`],
		[0, `&real;`],
		[0, `&reals;`],
		[0, `&rx;`],
		[3, `&trade;`],
		[1, `&integers;`],
		[2, `&mho;`],
		[0, `&zeetrf;`],
		[0, `&iiota;`],
		[2, `&bernou;`],
		[0, `&Cayleys;`],
		[1, `&escr;`],
		[0, `&Escr;`],
		[0, `&Fouriertrf;`],
		[1, `&Mellintrf;`],
		[0, `&order;`],
		[0, `&alefsym;`],
		[0, `&beth;`],
		[0, `&gimel;`],
		[0, `&daleth;`],
		[12, `&CapitalDifferentialD;`],
		[0, `&dd;`],
		[0, `&ee;`],
		[0, `&ii;`],
		[10, `&frac13;`],
		[0, `&frac23;`],
		[0, `&frac15;`],
		[0, `&frac25;`],
		[0, `&frac35;`],
		[0, `&frac45;`],
		[0, `&frac16;`],
		[0, `&frac56;`],
		[0, `&frac18;`],
		[0, `&frac38;`],
		[0, `&frac58;`],
		[0, `&frac78;`],
		[49, `&larr;`],
		[0, `&ShortUpArrow;`],
		[0, `&rarr;`],
		[0, `&darr;`],
		[0, `&harr;`],
		[0, `&updownarrow;`],
		[0, `&nwarr;`],
		[0, `&nearr;`],
		[0, `&LowerRightArrow;`],
		[0, `&LowerLeftArrow;`],
		[0, `&nlarr;`],
		[0, `&nrarr;`],
		[1, {
			v: `&rarrw;`,
			n: 824,
			o: `&nrarrw;`
		}],
		[0, `&Larr;`],
		[0, `&Uarr;`],
		[0, `&Rarr;`],
		[0, `&Darr;`],
		[0, `&larrtl;`],
		[0, `&rarrtl;`],
		[0, `&LeftTeeArrow;`],
		[0, `&mapstoup;`],
		[0, `&map;`],
		[0, `&DownTeeArrow;`],
		[1, `&hookleftarrow;`],
		[0, `&hookrightarrow;`],
		[0, `&larrlp;`],
		[0, `&looparrowright;`],
		[0, `&harrw;`],
		[0, `&nharr;`],
		[1, `&lsh;`],
		[0, `&rsh;`],
		[0, `&ldsh;`],
		[0, `&rdsh;`],
		[1, `&crarr;`],
		[0, `&cularr;`],
		[0, `&curarr;`],
		[2, `&circlearrowleft;`],
		[0, `&circlearrowright;`],
		[0, `&leftharpoonup;`],
		[0, `&DownLeftVector;`],
		[0, `&RightUpVector;`],
		[0, `&LeftUpVector;`],
		[0, `&rharu;`],
		[0, `&DownRightVector;`],
		[0, `&dharr;`],
		[0, `&dharl;`],
		[0, `&RightArrowLeftArrow;`],
		[0, `&udarr;`],
		[0, `&LeftArrowRightArrow;`],
		[0, `&leftleftarrows;`],
		[0, `&upuparrows;`],
		[0, `&rightrightarrows;`],
		[0, `&ddarr;`],
		[0, `&leftrightharpoons;`],
		[0, `&Equilibrium;`],
		[0, `&nlArr;`],
		[0, `&nhArr;`],
		[0, `&nrArr;`],
		[0, `&DoubleLeftArrow;`],
		[0, `&DoubleUpArrow;`],
		[0, `&DoubleRightArrow;`],
		[0, `&dArr;`],
		[0, `&DoubleLeftRightArrow;`],
		[0, `&DoubleUpDownArrow;`],
		[0, `&nwArr;`],
		[0, `&neArr;`],
		[0, `&seArr;`],
		[0, `&swArr;`],
		[0, `&lAarr;`],
		[0, `&rAarr;`],
		[1, `&zigrarr;`],
		[6, `&larrb;`],
		[0, `&rarrb;`],
		[15, `&DownArrowUpArrow;`],
		[7, `&loarr;`],
		[0, `&roarr;`],
		[0, `&hoarr;`],
		[0, `&forall;`],
		[0, `&comp;`],
		[0, {
			v: `&part;`,
			n: 824,
			o: `&npart;`
		}],
		[0, `&exist;`],
		[0, `&nexist;`],
		[0, `&empty;`],
		[1, `&Del;`],
		[0, `&Element;`],
		[0, `&NotElement;`],
		[1, `&ni;`],
		[0, `&notni;`],
		[2, `&prod;`],
		[0, `&coprod;`],
		[0, `&sum;`],
		[0, `&minus;`],
		[0, `&MinusPlus;`],
		[0, `&dotplus;`],
		[1, `&Backslash;`],
		[0, `&lowast;`],
		[0, `&compfn;`],
		[1, `&radic;`],
		[2, `&prop;`],
		[0, `&infin;`],
		[0, `&angrt;`],
		[0, {
			v: `&ang;`,
			n: 8402,
			o: `&nang;`
		}],
		[0, `&angmsd;`],
		[0, `&angsph;`],
		[0, `&mid;`],
		[0, `&nmid;`],
		[0, `&DoubleVerticalBar;`],
		[0, `&NotDoubleVerticalBar;`],
		[0, `&and;`],
		[0, `&or;`],
		[0, {
			v: `&cap;`,
			n: 65024,
			o: `&caps;`
		}],
		[0, {
			v: `&cup;`,
			n: 65024,
			o: `&cups;`
		}],
		[0, `&int;`],
		[0, `&Int;`],
		[0, `&iiint;`],
		[0, `&conint;`],
		[0, `&Conint;`],
		[0, `&Cconint;`],
		[0, `&cwint;`],
		[0, `&ClockwiseContourIntegral;`],
		[0, `&awconint;`],
		[0, `&there4;`],
		[0, `&becaus;`],
		[0, `&ratio;`],
		[0, `&Colon;`],
		[0, `&dotminus;`],
		[1, `&mDDot;`],
		[0, `&homtht;`],
		[0, {
			v: `&sim;`,
			n: 8402,
			o: `&nvsim;`
		}],
		[0, {
			v: `&backsim;`,
			n: 817,
			o: `&race;`
		}],
		[0, {
			v: `&ac;`,
			n: 819,
			o: `&acE;`
		}],
		[0, `&acd;`],
		[0, `&VerticalTilde;`],
		[0, `&NotTilde;`],
		[0, {
			v: `&eqsim;`,
			n: 824,
			o: `&nesim;`
		}],
		[0, `&sime;`],
		[0, `&NotTildeEqual;`],
		[0, `&cong;`],
		[0, `&simne;`],
		[0, `&ncong;`],
		[0, `&ap;`],
		[0, `&nap;`],
		[0, `&ape;`],
		[0, {
			v: `&apid;`,
			n: 824,
			o: `&napid;`
		}],
		[0, `&backcong;`],
		[0, {
			v: `&asympeq;`,
			n: 8402,
			o: `&nvap;`
		}],
		[0, {
			v: `&bump;`,
			n: 824,
			o: `&nbump;`
		}],
		[0, {
			v: `&bumpe;`,
			n: 824,
			o: `&nbumpe;`
		}],
		[0, {
			v: `&doteq;`,
			n: 824,
			o: `&nedot;`
		}],
		[0, `&doteqdot;`],
		[0, `&efDot;`],
		[0, `&erDot;`],
		[0, `&Assign;`],
		[0, `&ecolon;`],
		[0, `&ecir;`],
		[0, `&circeq;`],
		[1, `&wedgeq;`],
		[0, `&veeeq;`],
		[1, `&triangleq;`],
		[2, `&equest;`],
		[0, `&ne;`],
		[0, {
			v: `&Congruent;`,
			n: 8421,
			o: `&bnequiv;`
		}],
		[0, `&nequiv;`],
		[1, {
			v: `&le;`,
			n: 8402,
			o: `&nvle;`
		}],
		[0, {
			v: `&ge;`,
			n: 8402,
			o: `&nvge;`
		}],
		[0, {
			v: `&lE;`,
			n: 824,
			o: `&nlE;`
		}],
		[0, {
			v: `&gE;`,
			n: 824,
			o: `&ngE;`
		}],
		[0, {
			v: `&lnE;`,
			n: 65024,
			o: `&lvertneqq;`
		}],
		[0, {
			v: `&gnE;`,
			n: 65024,
			o: `&gvertneqq;`
		}],
		[0, {
			v: `&ll;`,
			n: new Map(t([[824, `&nLtv;`], [7577, `&nLt;`]]))
		}],
		[0, {
			v: `&gg;`,
			n: new Map(t([[824, `&nGtv;`], [7577, `&nGt;`]]))
		}],
		[0, `&between;`],
		[0, `&NotCupCap;`],
		[0, `&nless;`],
		[0, `&ngt;`],
		[0, `&nle;`],
		[0, `&nge;`],
		[0, `&lesssim;`],
		[0, `&GreaterTilde;`],
		[0, `&nlsim;`],
		[0, `&ngsim;`],
		[0, `&LessGreater;`],
		[0, `&gl;`],
		[0, `&NotLessGreater;`],
		[0, `&NotGreaterLess;`],
		[0, `&pr;`],
		[0, `&sc;`],
		[0, `&prcue;`],
		[0, `&sccue;`],
		[0, `&PrecedesTilde;`],
		[0, {
			v: `&scsim;`,
			n: 824,
			o: `&NotSucceedsTilde;`
		}],
		[0, `&NotPrecedes;`],
		[0, `&NotSucceeds;`],
		[0, {
			v: `&sub;`,
			n: 8402,
			o: `&NotSubset;`
		}],
		[0, {
			v: `&sup;`,
			n: 8402,
			o: `&NotSuperset;`
		}],
		[0, `&nsub;`],
		[0, `&nsup;`],
		[0, `&sube;`],
		[0, `&supe;`],
		[0, `&NotSubsetEqual;`],
		[0, `&NotSupersetEqual;`],
		[0, {
			v: `&subne;`,
			n: 65024,
			o: `&varsubsetneq;`
		}],
		[0, {
			v: `&supne;`,
			n: 65024,
			o: `&varsupsetneq;`
		}],
		[1, `&cupdot;`],
		[0, `&UnionPlus;`],
		[0, {
			v: `&sqsub;`,
			n: 824,
			o: `&NotSquareSubset;`
		}],
		[0, {
			v: `&sqsup;`,
			n: 824,
			o: `&NotSquareSuperset;`
		}],
		[0, `&sqsube;`],
		[0, `&sqsupe;`],
		[0, {
			v: `&sqcap;`,
			n: 65024,
			o: `&sqcaps;`
		}],
		[0, {
			v: `&sqcup;`,
			n: 65024,
			o: `&sqcups;`
		}],
		[0, `&CirclePlus;`],
		[0, `&CircleMinus;`],
		[0, `&CircleTimes;`],
		[0, `&osol;`],
		[0, `&CircleDot;`],
		[0, `&circledcirc;`],
		[0, `&circledast;`],
		[1, `&circleddash;`],
		[0, `&boxplus;`],
		[0, `&boxminus;`],
		[0, `&boxtimes;`],
		[0, `&dotsquare;`],
		[0, `&RightTee;`],
		[0, `&dashv;`],
		[0, `&DownTee;`],
		[0, `&bot;`],
		[1, `&models;`],
		[0, `&DoubleRightTee;`],
		[0, `&Vdash;`],
		[0, `&Vvdash;`],
		[0, `&VDash;`],
		[0, `&nvdash;`],
		[0, `&nvDash;`],
		[0, `&nVdash;`],
		[0, `&nVDash;`],
		[0, `&prurel;`],
		[1, `&LeftTriangle;`],
		[0, `&RightTriangle;`],
		[0, {
			v: `&LeftTriangleEqual;`,
			n: 8402,
			o: `&nvltrie;`
		}],
		[0, {
			v: `&RightTriangleEqual;`,
			n: 8402,
			o: `&nvrtrie;`
		}],
		[0, `&origof;`],
		[0, `&imof;`],
		[0, `&multimap;`],
		[0, `&hercon;`],
		[0, `&intcal;`],
		[0, `&veebar;`],
		[1, `&barvee;`],
		[0, `&angrtvb;`],
		[0, `&lrtri;`],
		[0, `&bigwedge;`],
		[0, `&bigvee;`],
		[0, `&bigcap;`],
		[0, `&bigcup;`],
		[0, `&diam;`],
		[0, `&sdot;`],
		[0, `&sstarf;`],
		[0, `&divideontimes;`],
		[0, `&bowtie;`],
		[0, `&ltimes;`],
		[0, `&rtimes;`],
		[0, `&leftthreetimes;`],
		[0, `&rightthreetimes;`],
		[0, `&backsimeq;`],
		[0, `&curlyvee;`],
		[0, `&curlywedge;`],
		[0, `&Sub;`],
		[0, `&Sup;`],
		[0, `&Cap;`],
		[0, `&Cup;`],
		[0, `&fork;`],
		[0, `&epar;`],
		[0, `&lessdot;`],
		[0, `&gtdot;`],
		[0, {
			v: `&Ll;`,
			n: 824,
			o: `&nLl;`
		}],
		[0, {
			v: `&Gg;`,
			n: 824,
			o: `&nGg;`
		}],
		[0, {
			v: `&leg;`,
			n: 65024,
			o: `&lesg;`
		}],
		[0, {
			v: `&gel;`,
			n: 65024,
			o: `&gesl;`
		}],
		[2, `&cuepr;`],
		[0, `&cuesc;`],
		[0, `&NotPrecedesSlantEqual;`],
		[0, `&NotSucceedsSlantEqual;`],
		[0, `&NotSquareSubsetEqual;`],
		[0, `&NotSquareSupersetEqual;`],
		[2, `&lnsim;`],
		[0, `&gnsim;`],
		[0, `&precnsim;`],
		[0, `&scnsim;`],
		[0, `&nltri;`],
		[0, `&NotRightTriangle;`],
		[0, `&nltrie;`],
		[0, `&NotRightTriangleEqual;`],
		[0, `&vellip;`],
		[0, `&ctdot;`],
		[0, `&utdot;`],
		[0, `&dtdot;`],
		[0, `&disin;`],
		[0, `&isinsv;`],
		[0, `&isins;`],
		[0, {
			v: `&isindot;`,
			n: 824,
			o: `&notindot;`
		}],
		[0, `&notinvc;`],
		[0, `&notinvb;`],
		[1, {
			v: `&isinE;`,
			n: 824,
			o: `&notinE;`
		}],
		[0, `&nisd;`],
		[0, `&xnis;`],
		[0, `&nis;`],
		[0, `&notnivc;`],
		[0, `&notnivb;`],
		[6, `&barwed;`],
		[0, `&Barwed;`],
		[1, `&lceil;`],
		[0, `&rceil;`],
		[0, `&LeftFloor;`],
		[0, `&rfloor;`],
		[0, `&drcrop;`],
		[0, `&dlcrop;`],
		[0, `&urcrop;`],
		[0, `&ulcrop;`],
		[0, `&bnot;`],
		[1, `&profline;`],
		[0, `&profsurf;`],
		[1, `&telrec;`],
		[0, `&target;`],
		[5, `&ulcorn;`],
		[0, `&urcorn;`],
		[0, `&dlcorn;`],
		[0, `&drcorn;`],
		[2, `&frown;`],
		[0, `&smile;`],
		[9, `&cylcty;`],
		[0, `&profalar;`],
		[7, `&topbot;`],
		[6, `&ovbar;`],
		[1, `&solbar;`],
		[60, `&angzarr;`],
		[51, `&lmoustache;`],
		[0, `&rmoustache;`],
		[2, `&OverBracket;`],
		[0, `&bbrk;`],
		[0, `&bbrktbrk;`],
		[37, `&OverParenthesis;`],
		[0, `&UnderParenthesis;`],
		[0, `&OverBrace;`],
		[0, `&UnderBrace;`],
		[2, `&trpezium;`],
		[4, `&elinters;`],
		[59, `&blank;`],
		[164, `&circledS;`],
		[55, `&boxh;`],
		[1, `&boxv;`],
		[9, `&boxdr;`],
		[3, `&boxdl;`],
		[3, `&boxur;`],
		[3, `&boxul;`],
		[3, `&boxvr;`],
		[7, `&boxvl;`],
		[7, `&boxhd;`],
		[7, `&boxhu;`],
		[7, `&boxvh;`],
		[19, `&boxH;`],
		[0, `&boxV;`],
		[0, `&boxdR;`],
		[0, `&boxDr;`],
		[0, `&boxDR;`],
		[0, `&boxdL;`],
		[0, `&boxDl;`],
		[0, `&boxDL;`],
		[0, `&boxuR;`],
		[0, `&boxUr;`],
		[0, `&boxUR;`],
		[0, `&boxuL;`],
		[0, `&boxUl;`],
		[0, `&boxUL;`],
		[0, `&boxvR;`],
		[0, `&boxVr;`],
		[0, `&boxVR;`],
		[0, `&boxvL;`],
		[0, `&boxVl;`],
		[0, `&boxVL;`],
		[0, `&boxHd;`],
		[0, `&boxhD;`],
		[0, `&boxHD;`],
		[0, `&boxHu;`],
		[0, `&boxhU;`],
		[0, `&boxHU;`],
		[0, `&boxvH;`],
		[0, `&boxVh;`],
		[0, `&boxVH;`],
		[19, `&uhblk;`],
		[3, `&lhblk;`],
		[3, `&block;`],
		[8, `&blk14;`],
		[0, `&blk12;`],
		[0, `&blk34;`],
		[13, `&square;`],
		[8, `&blacksquare;`],
		[0, `&EmptyVerySmallSquare;`],
		[1, `&rect;`],
		[0, `&marker;`],
		[2, `&fltns;`],
		[1, `&bigtriangleup;`],
		[0, `&blacktriangle;`],
		[0, `&triangle;`],
		[2, `&blacktriangleright;`],
		[0, `&rtri;`],
		[3, `&bigtriangledown;`],
		[0, `&blacktriangledown;`],
		[0, `&dtri;`],
		[2, `&blacktriangleleft;`],
		[0, `&ltri;`],
		[6, `&loz;`],
		[0, `&cir;`],
		[32, `&tridot;`],
		[2, `&bigcirc;`],
		[8, `&ultri;`],
		[0, `&urtri;`],
		[0, `&lltri;`],
		[0, `&EmptySmallSquare;`],
		[0, `&FilledSmallSquare;`],
		[8, `&bigstar;`],
		[0, `&star;`],
		[7, `&phone;`],
		[49, `&female;`],
		[1, `&male;`],
		[29, `&spades;`],
		[2, `&clubs;`],
		[1, `&hearts;`],
		[0, `&diamondsuit;`],
		[3, `&sung;`],
		[2, `&flat;`],
		[0, `&natural;`],
		[0, `&sharp;`],
		[163, `&check;`],
		[3, `&cross;`],
		[8, `&malt;`],
		[21, `&sext;`],
		[33, `&VerticalSeparator;`],
		[25, `&lbbrk;`],
		[0, `&rbbrk;`],
		[84, `&bsolhsub;`],
		[0, `&suphsol;`],
		[28, `&LeftDoubleBracket;`],
		[0, `&RightDoubleBracket;`],
		[0, `&lang;`],
		[0, `&rang;`],
		[0, `&Lang;`],
		[0, `&Rang;`],
		[0, `&loang;`],
		[0, `&roang;`],
		[7, `&longleftarrow;`],
		[0, `&longrightarrow;`],
		[0, `&longleftrightarrow;`],
		[0, `&DoubleLongLeftArrow;`],
		[0, `&DoubleLongRightArrow;`],
		[0, `&DoubleLongLeftRightArrow;`],
		[1, `&longmapsto;`],
		[2, `&dzigrarr;`],
		[258, `&nvlArr;`],
		[0, `&nvrArr;`],
		[0, `&nvHarr;`],
		[0, `&Map;`],
		[6, `&lbarr;`],
		[0, `&bkarow;`],
		[0, `&lBarr;`],
		[0, `&dbkarow;`],
		[0, `&drbkarow;`],
		[0, `&DDotrahd;`],
		[0, `&UpArrowBar;`],
		[0, `&DownArrowBar;`],
		[2, `&Rarrtl;`],
		[2, `&latail;`],
		[0, `&ratail;`],
		[0, `&lAtail;`],
		[0, `&rAtail;`],
		[0, `&larrfs;`],
		[0, `&rarrfs;`],
		[0, `&larrbfs;`],
		[0, `&rarrbfs;`],
		[2, `&nwarhk;`],
		[0, `&nearhk;`],
		[0, `&hksearow;`],
		[0, `&hkswarow;`],
		[0, `&nwnear;`],
		[0, `&nesear;`],
		[0, `&seswar;`],
		[0, `&swnwar;`],
		[8, {
			v: `&rarrc;`,
			n: 824,
			o: `&nrarrc;`
		}],
		[1, `&cudarrr;`],
		[0, `&ldca;`],
		[0, `&rdca;`],
		[0, `&cudarrl;`],
		[0, `&larrpl;`],
		[2, `&curarrm;`],
		[0, `&cularrp;`],
		[7, `&rarrpl;`],
		[2, `&harrcir;`],
		[0, `&Uarrocir;`],
		[0, `&lurdshar;`],
		[0, `&ldrushar;`],
		[2, `&LeftRightVector;`],
		[0, `&RightUpDownVector;`],
		[0, `&DownLeftRightVector;`],
		[0, `&LeftUpDownVector;`],
		[0, `&LeftVectorBar;`],
		[0, `&RightVectorBar;`],
		[0, `&RightUpVectorBar;`],
		[0, `&RightDownVectorBar;`],
		[0, `&DownLeftVectorBar;`],
		[0, `&DownRightVectorBar;`],
		[0, `&LeftUpVectorBar;`],
		[0, `&LeftDownVectorBar;`],
		[0, `&LeftTeeVector;`],
		[0, `&RightTeeVector;`],
		[0, `&RightUpTeeVector;`],
		[0, `&RightDownTeeVector;`],
		[0, `&DownLeftTeeVector;`],
		[0, `&DownRightTeeVector;`],
		[0, `&LeftUpTeeVector;`],
		[0, `&LeftDownTeeVector;`],
		[0, `&lHar;`],
		[0, `&uHar;`],
		[0, `&rHar;`],
		[0, `&dHar;`],
		[0, `&luruhar;`],
		[0, `&ldrdhar;`],
		[0, `&ruluhar;`],
		[0, `&rdldhar;`],
		[0, `&lharul;`],
		[0, `&llhard;`],
		[0, `&rharul;`],
		[0, `&lrhard;`],
		[0, `&udhar;`],
		[0, `&duhar;`],
		[0, `&RoundImplies;`],
		[0, `&erarr;`],
		[0, `&simrarr;`],
		[0, `&larrsim;`],
		[0, `&rarrsim;`],
		[0, `&rarrap;`],
		[0, `&ltlarr;`],
		[1, `&gtrarr;`],
		[0, `&subrarr;`],
		[1, `&suplarr;`],
		[0, `&lfisht;`],
		[0, `&rfisht;`],
		[0, `&ufisht;`],
		[0, `&dfisht;`],
		[5, `&lopar;`],
		[0, `&ropar;`],
		[4, `&lbrke;`],
		[0, `&rbrke;`],
		[0, `&lbrkslu;`],
		[0, `&rbrksld;`],
		[0, `&lbrksld;`],
		[0, `&rbrkslu;`],
		[0, `&langd;`],
		[0, `&rangd;`],
		[0, `&lparlt;`],
		[0, `&rpargt;`],
		[0, `&gtlPar;`],
		[0, `&ltrPar;`],
		[3, `&vzigzag;`],
		[1, `&vangrt;`],
		[0, `&angrtvbd;`],
		[6, `&ange;`],
		[0, `&range;`],
		[0, `&dwangle;`],
		[0, `&uwangle;`],
		[0, `&angmsdaa;`],
		[0, `&angmsdab;`],
		[0, `&angmsdac;`],
		[0, `&angmsdad;`],
		[0, `&angmsdae;`],
		[0, `&angmsdaf;`],
		[0, `&angmsdag;`],
		[0, `&angmsdah;`],
		[0, `&bemptyv;`],
		[0, `&demptyv;`],
		[0, `&cemptyv;`],
		[0, `&raemptyv;`],
		[0, `&laemptyv;`],
		[0, `&ohbar;`],
		[0, `&omid;`],
		[0, `&opar;`],
		[1, `&operp;`],
		[1, `&olcross;`],
		[0, `&odsold;`],
		[1, `&olcir;`],
		[0, `&ofcir;`],
		[0, `&olt;`],
		[0, `&ogt;`],
		[0, `&cirscir;`],
		[0, `&cirE;`],
		[0, `&solb;`],
		[0, `&bsolb;`],
		[3, `&boxbox;`],
		[3, `&trisb;`],
		[0, `&rtriltri;`],
		[0, {
			v: `&LeftTriangleBar;`,
			n: 824,
			o: `&NotLeftTriangleBar;`
		}],
		[0, {
			v: `&RightTriangleBar;`,
			n: 824,
			o: `&NotRightTriangleBar;`
		}],
		[11, `&iinfin;`],
		[0, `&infintie;`],
		[0, `&nvinfin;`],
		[4, `&eparsl;`],
		[0, `&smeparsl;`],
		[0, `&eqvparsl;`],
		[5, `&blacklozenge;`],
		[8, `&RuleDelayed;`],
		[1, `&dsol;`],
		[9, `&bigodot;`],
		[0, `&bigoplus;`],
		[0, `&bigotimes;`],
		[1, `&biguplus;`],
		[1, `&bigsqcup;`],
		[5, `&iiiint;`],
		[0, `&fpartint;`],
		[2, `&cirfnint;`],
		[0, `&awint;`],
		[0, `&rppolint;`],
		[0, `&scpolint;`],
		[0, `&npolint;`],
		[0, `&pointint;`],
		[0, `&quatint;`],
		[0, `&intlarhk;`],
		[10, `&pluscir;`],
		[0, `&plusacir;`],
		[0, `&simplus;`],
		[0, `&plusdu;`],
		[0, `&plussim;`],
		[0, `&plustwo;`],
		[1, `&mcomma;`],
		[0, `&minusdu;`],
		[2, `&loplus;`],
		[0, `&roplus;`],
		[0, `&Cross;`],
		[0, `&timesd;`],
		[0, `&timesbar;`],
		[1, `&smashp;`],
		[0, `&lotimes;`],
		[0, `&rotimes;`],
		[0, `&otimesas;`],
		[0, `&Otimes;`],
		[0, `&odiv;`],
		[0, `&triplus;`],
		[0, `&triminus;`],
		[0, `&tritime;`],
		[0, `&intprod;`],
		[2, `&amalg;`],
		[0, `&capdot;`],
		[1, `&ncup;`],
		[0, `&ncap;`],
		[0, `&capand;`],
		[0, `&cupor;`],
		[0, `&cupcap;`],
		[0, `&capcup;`],
		[0, `&cupbrcap;`],
		[0, `&capbrcup;`],
		[0, `&cupcup;`],
		[0, `&capcap;`],
		[0, `&ccups;`],
		[0, `&ccaps;`],
		[2, `&ccupssm;`],
		[2, `&And;`],
		[0, `&Or;`],
		[0, `&andand;`],
		[0, `&oror;`],
		[0, `&orslope;`],
		[0, `&andslope;`],
		[1, `&andv;`],
		[0, `&orv;`],
		[0, `&andd;`],
		[0, `&ord;`],
		[1, `&wedbar;`],
		[6, `&sdote;`],
		[3, `&simdot;`],
		[2, {
			v: `&congdot;`,
			n: 824,
			o: `&ncongdot;`
		}],
		[0, `&easter;`],
		[0, `&apacir;`],
		[0, {
			v: `&apE;`,
			n: 824,
			o: `&napE;`
		}],
		[0, `&eplus;`],
		[0, `&pluse;`],
		[0, `&Esim;`],
		[0, `&Colone;`],
		[0, `&Equal;`],
		[1, `&ddotseq;`],
		[0, `&equivDD;`],
		[0, `&ltcir;`],
		[0, `&gtcir;`],
		[0, `&ltquest;`],
		[0, `&gtquest;`],
		[0, {
			v: `&leqslant;`,
			n: 824,
			o: `&nleqslant;`
		}],
		[0, {
			v: `&geqslant;`,
			n: 824,
			o: `&ngeqslant;`
		}],
		[0, `&lesdot;`],
		[0, `&gesdot;`],
		[0, `&lesdoto;`],
		[0, `&gesdoto;`],
		[0, `&lesdotor;`],
		[0, `&gesdotol;`],
		[0, `&lap;`],
		[0, `&gap;`],
		[0, `&lne;`],
		[0, `&gne;`],
		[0, `&lnap;`],
		[0, `&gnap;`],
		[0, `&lEg;`],
		[0, `&gEl;`],
		[0, `&lsime;`],
		[0, `&gsime;`],
		[0, `&lsimg;`],
		[0, `&gsiml;`],
		[0, `&lgE;`],
		[0, `&glE;`],
		[0, `&lesges;`],
		[0, `&gesles;`],
		[0, `&els;`],
		[0, `&egs;`],
		[0, `&elsdot;`],
		[0, `&egsdot;`],
		[0, `&el;`],
		[0, `&eg;`],
		[2, `&siml;`],
		[0, `&simg;`],
		[0, `&simlE;`],
		[0, `&simgE;`],
		[0, {
			v: `&LessLess;`,
			n: 824,
			o: `&NotNestedLessLess;`
		}],
		[0, {
			v: `&GreaterGreater;`,
			n: 824,
			o: `&NotNestedGreaterGreater;`
		}],
		[1, `&glj;`],
		[0, `&gla;`],
		[0, `&ltcc;`],
		[0, `&gtcc;`],
		[0, `&lescc;`],
		[0, `&gescc;`],
		[0, `&smt;`],
		[0, `&lat;`],
		[0, {
			v: `&smte;`,
			n: 65024,
			o: `&smtes;`
		}],
		[0, {
			v: `&late;`,
			n: 65024,
			o: `&lates;`
		}],
		[0, `&bumpE;`],
		[0, {
			v: `&PrecedesEqual;`,
			n: 824,
			o: `&NotPrecedesEqual;`
		}],
		[0, {
			v: `&sce;`,
			n: 824,
			o: `&NotSucceedsEqual;`
		}],
		[2, `&prE;`],
		[0, `&scE;`],
		[0, `&precneqq;`],
		[0, `&scnE;`],
		[0, `&prap;`],
		[0, `&scap;`],
		[0, `&precnapprox;`],
		[0, `&scnap;`],
		[0, `&Pr;`],
		[0, `&Sc;`],
		[0, `&subdot;`],
		[0, `&supdot;`],
		[0, `&subplus;`],
		[0, `&supplus;`],
		[0, `&submult;`],
		[0, `&supmult;`],
		[0, `&subedot;`],
		[0, `&supedot;`],
		[0, {
			v: `&subE;`,
			n: 824,
			o: `&nsubE;`
		}],
		[0, {
			v: `&supE;`,
			n: 824,
			o: `&nsupE;`
		}],
		[0, `&subsim;`],
		[0, `&supsim;`],
		[2, {
			v: `&subnE;`,
			n: 65024,
			o: `&varsubsetneqq;`
		}],
		[0, {
			v: `&supnE;`,
			n: 65024,
			o: `&varsupsetneqq;`
		}],
		[2, `&csub;`],
		[0, `&csup;`],
		[0, `&csube;`],
		[0, `&csupe;`],
		[0, `&subsup;`],
		[0, `&supsub;`],
		[0, `&subsub;`],
		[0, `&supsup;`],
		[0, `&suphsub;`],
		[0, `&supdsub;`],
		[0, `&forkv;`],
		[0, `&topfork;`],
		[0, `&mlcp;`],
		[8, `&Dashv;`],
		[1, `&Vdashl;`],
		[0, `&Barv;`],
		[0, `&vBar;`],
		[0, `&vBarv;`],
		[1, `&Vbar;`],
		[0, `&Not;`],
		[0, `&bNot;`],
		[0, `&rnmid;`],
		[0, `&cirmid;`],
		[0, `&midcir;`],
		[0, `&topcir;`],
		[0, `&nhpar;`],
		[0, `&parsim;`],
		[9, {
			v: `&parsl;`,
			n: 8421,
			o: `&nparsl;`
		}],
		[44343, { n: new Map(t([
			[56476, `&Ascr;`],
			[1, `&Cscr;`],
			[0, `&Dscr;`],
			[2, `&Gscr;`],
			[2, `&Jscr;`],
			[0, `&Kscr;`],
			[2, `&Nscr;`],
			[0, `&Oscr;`],
			[0, `&Pscr;`],
			[0, `&Qscr;`],
			[1, `&Sscr;`],
			[0, `&Tscr;`],
			[0, `&Uscr;`],
			[0, `&Vscr;`],
			[0, `&Wscr;`],
			[0, `&Xscr;`],
			[0, `&Yscr;`],
			[0, `&Zscr;`],
			[0, `&ascr;`],
			[0, `&bscr;`],
			[0, `&cscr;`],
			[0, `&dscr;`],
			[1, `&fscr;`],
			[1, `&hscr;`],
			[0, `&iscr;`],
			[0, `&jscr;`],
			[0, `&kscr;`],
			[0, `&lscr;`],
			[0, `&mscr;`],
			[0, `&nscr;`],
			[1, `&pscr;`],
			[0, `&qscr;`],
			[0, `&rscr;`],
			[0, `&sscr;`],
			[0, `&tscr;`],
			[0, `&uscr;`],
			[0, `&vscr;`],
			[0, `&wscr;`],
			[0, `&xscr;`],
			[0, `&yscr;`],
			[0, `&zscr;`],
			[52, `&Afr;`],
			[0, `&Bfr;`],
			[1, `&Dfr;`],
			[0, `&Efr;`],
			[0, `&Ffr;`],
			[0, `&Gfr;`],
			[2, `&Jfr;`],
			[0, `&Kfr;`],
			[0, `&Lfr;`],
			[0, `&Mfr;`],
			[0, `&Nfr;`],
			[0, `&Ofr;`],
			[0, `&Pfr;`],
			[0, `&Qfr;`],
			[1, `&Sfr;`],
			[0, `&Tfr;`],
			[0, `&Ufr;`],
			[0, `&Vfr;`],
			[0, `&Wfr;`],
			[0, `&Xfr;`],
			[0, `&Yfr;`],
			[1, `&afr;`],
			[0, `&bfr;`],
			[0, `&cfr;`],
			[0, `&dfr;`],
			[0, `&efr;`],
			[0, `&ffr;`],
			[0, `&gfr;`],
			[0, `&hfr;`],
			[0, `&ifr;`],
			[0, `&jfr;`],
			[0, `&kfr;`],
			[0, `&lfr;`],
			[0, `&mfr;`],
			[0, `&nfr;`],
			[0, `&ofr;`],
			[0, `&pfr;`],
			[0, `&qfr;`],
			[0, `&rfr;`],
			[0, `&sfr;`],
			[0, `&tfr;`],
			[0, `&ufr;`],
			[0, `&vfr;`],
			[0, `&wfr;`],
			[0, `&xfr;`],
			[0, `&yfr;`],
			[0, `&zfr;`],
			[0, `&Aopf;`],
			[0, `&Bopf;`],
			[1, `&Dopf;`],
			[0, `&Eopf;`],
			[0, `&Fopf;`],
			[0, `&Gopf;`],
			[1, `&Iopf;`],
			[0, `&Jopf;`],
			[0, `&Kopf;`],
			[0, `&Lopf;`],
			[0, `&Mopf;`],
			[1, `&Oopf;`],
			[3, `&Sopf;`],
			[0, `&Topf;`],
			[0, `&Uopf;`],
			[0, `&Vopf;`],
			[0, `&Wopf;`],
			[0, `&Xopf;`],
			[0, `&Yopf;`],
			[1, `&aopf;`],
			[0, `&bopf;`],
			[0, `&copf;`],
			[0, `&dopf;`],
			[0, `&eopf;`],
			[0, `&fopf;`],
			[0, `&gopf;`],
			[0, `&hopf;`],
			[0, `&iopf;`],
			[0, `&jopf;`],
			[0, `&kopf;`],
			[0, `&lopf;`],
			[0, `&mopf;`],
			[0, `&nopf;`],
			[0, `&oopf;`],
			[0, `&popf;`],
			[0, `&qopf;`],
			[0, `&ropf;`],
			[0, `&sopf;`],
			[0, `&topf;`],
			[0, `&uopf;`],
			[0, `&vopf;`],
			[0, `&wopf;`],
			[0, `&xopf;`],
			[0, `&yopf;`],
			[0, `&zopf;`]
		])) }],
		[8906, `&fflig;`],
		[0, `&filig;`],
		[0, `&fllig;`],
		[0, `&ffilig;`],
		[0, `&ffllig;`]
	]));
})), p = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.escapeText = e.escapeAttribute = e.escapeUTF8 = e.escape = e.encodeXML = e.getCodePoint = e.xmlReplacer = void 0, e.xmlReplacer = /["&'<>$\x80-\uFFFF]/g;
	var t = /* @__PURE__ */ new Map([
		[34, `&quot;`],
		[38, `&amp;`],
		[39, `&apos;`],
		[60, `&lt;`],
		[62, `&gt;`]
	]);
	e.getCodePoint = String.prototype.codePointAt == null ? function(e, t) {
		return (e.charCodeAt(t) & 64512) == 55296 ? (e.charCodeAt(t) - 55296) * 1024 + e.charCodeAt(t + 1) - 56320 + 65536 : e.charCodeAt(t);
	} : function(e, t) {
		return e.codePointAt(t);
	};
	function n(n) {
		for (var r = ``, i = 0, a; (a = e.xmlReplacer.exec(n)) !== null;) {
			var o = a.index, s = n.charCodeAt(o), c = t.get(s);
			c === void 0 ? (r += `${n.substring(i, o)}&#x${(0, e.getCodePoint)(n, o).toString(16)};`, i = e.xmlReplacer.lastIndex += Number((s & 64512) == 55296)) : (r += n.substring(i, o) + c, i = o + 1);
		}
		return r + n.substr(i);
	}
	e.encodeXML = n, e.escape = n;
	function r(e, t) {
		return function(n) {
			for (var r, i = 0, a = ``; r = e.exec(n);) i !== r.index && (a += n.substring(i, r.index)), a += t.get(r[0].charCodeAt(0)), i = r.index + 1;
			return a + n.substring(i);
		};
	}
	e.escapeUTF8 = r(/[&<>'"]/g, t), e.escapeAttribute = r(/["&\u00A0]/g, /* @__PURE__ */ new Map([
		[34, `&quot;`],
		[38, `&amp;`],
		[160, `&nbsp;`]
	])), e.escapeText = r(/[&<>\u00A0]/g, /* @__PURE__ */ new Map([
		[38, `&amp;`],
		[60, `&lt;`],
		[62, `&gt;`],
		[160, `&nbsp;`]
	]));
})), m = e(((e) => {
	var t = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.encodeNonAsciiHTML = e.encodeHTML = void 0;
	var n = t(f()), r = p(), i = /[\t\n!-,./:-@[-`\f{-}$\x80-\uFFFF]/g;
	function a(e) {
		return s(i, e);
	}
	e.encodeHTML = a;
	function o(e) {
		return s(r.xmlReplacer, e);
	}
	e.encodeNonAsciiHTML = o;
	function s(e, t) {
		for (var i = ``, a = 0, o; (o = e.exec(t)) !== null;) {
			var s = o.index;
			i += t.substring(a, s);
			var c = t.charCodeAt(s), l = n.default.get(c);
			if (typeof l == `object`) {
				if (s + 1 < t.length) {
					var u = t.charCodeAt(s + 1), d = typeof l.n == `number` ? l.n === u ? l.o : void 0 : l.n.get(u);
					if (d !== void 0) {
						i += d, a = e.lastIndex += 1;
						continue;
					}
				}
				l = l.v;
			}
			if (l !== void 0) i += l, a = s + 1;
			else {
				var f = (0, r.getCodePoint)(t, s);
				i += `&#x${f.toString(16)};`, a = e.lastIndex += Number(f !== c);
			}
		}
		return i + t.substr(a);
	}
})), h = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.decodeXMLStrict = e.decodeHTML5Strict = e.decodeHTML4Strict = e.decodeHTML5 = e.decodeHTML4 = e.decodeHTMLAttribute = e.decodeHTMLStrict = e.decodeHTML = e.decodeXML = e.DecodingMode = e.EntityDecoder = e.encodeHTML5 = e.encodeHTML4 = e.encodeNonAsciiHTML = e.encodeHTML = e.escapeText = e.escapeAttribute = e.escapeUTF8 = e.escape = e.encodeXML = e.encode = e.decodeStrict = e.decode = e.EncodingMode = e.EntityLevel = void 0;
	var t = d(), n = m(), r = p(), i;
	(function(e) {
		e[e.XML = 0] = `XML`, e[e.HTML = 1] = `HTML`;
	})(i = e.EntityLevel ||= {});
	var a;
	(function(e) {
		e[e.UTF8 = 0] = `UTF8`, e[e.ASCII = 1] = `ASCII`, e[e.Extensive = 2] = `Extensive`, e[e.Attribute = 3] = `Attribute`, e[e.Text = 4] = `Text`;
	})(a = e.EncodingMode ||= {});
	function o(e, n) {
		if (n === void 0 && (n = i.XML), (typeof n == `number` ? n : n.level) === i.HTML) {
			var r = typeof n == `object` ? n.mode : void 0;
			return (0, t.decodeHTML)(e, r);
		}
		return (0, t.decodeXML)(e);
	}
	e.decode = o;
	function s(e, n) {
		n === void 0 && (n = i.XML);
		var r = typeof n == `number` ? { level: n } : n;
		return r.mode ??= t.DecodingMode.Strict, o(e, r);
	}
	e.decodeStrict = s;
	function c(e, t) {
		t === void 0 && (t = i.XML);
		var o = typeof t == `number` ? { level: t } : t;
		return o.mode === a.UTF8 ? (0, r.escapeUTF8)(e) : o.mode === a.Attribute ? (0, r.escapeAttribute)(e) : o.mode === a.Text ? (0, r.escapeText)(e) : o.level === i.HTML ? o.mode === a.ASCII ? (0, n.encodeNonAsciiHTML)(e) : (0, n.encodeHTML)(e) : (0, r.encodeXML)(e);
	}
	e.encode = c;
	var l = p();
	Object.defineProperty(e, "encodeXML", {
		enumerable: !0,
		get: function() {
			return l.encodeXML;
		}
	}), Object.defineProperty(e, "escape", {
		enumerable: !0,
		get: function() {
			return l.escape;
		}
	}), Object.defineProperty(e, "escapeUTF8", {
		enumerable: !0,
		get: function() {
			return l.escapeUTF8;
		}
	}), Object.defineProperty(e, "escapeAttribute", {
		enumerable: !0,
		get: function() {
			return l.escapeAttribute;
		}
	}), Object.defineProperty(e, "escapeText", {
		enumerable: !0,
		get: function() {
			return l.escapeText;
		}
	});
	var u = m();
	Object.defineProperty(e, "encodeHTML", {
		enumerable: !0,
		get: function() {
			return u.encodeHTML;
		}
	}), Object.defineProperty(e, "encodeNonAsciiHTML", {
		enumerable: !0,
		get: function() {
			return u.encodeNonAsciiHTML;
		}
	}), Object.defineProperty(e, "encodeHTML4", {
		enumerable: !0,
		get: function() {
			return u.encodeHTML;
		}
	}), Object.defineProperty(e, "encodeHTML5", {
		enumerable: !0,
		get: function() {
			return u.encodeHTML;
		}
	});
	var f = d();
	Object.defineProperty(e, "EntityDecoder", {
		enumerable: !0,
		get: function() {
			return f.EntityDecoder;
		}
	}), Object.defineProperty(e, "DecodingMode", {
		enumerable: !0,
		get: function() {
			return f.DecodingMode;
		}
	}), Object.defineProperty(e, "decodeXML", {
		enumerable: !0,
		get: function() {
			return f.decodeXML;
		}
	}), Object.defineProperty(e, "decodeHTML", {
		enumerable: !0,
		get: function() {
			return f.decodeHTML;
		}
	}), Object.defineProperty(e, "decodeHTMLStrict", {
		enumerable: !0,
		get: function() {
			return f.decodeHTMLStrict;
		}
	}), Object.defineProperty(e, "decodeHTMLAttribute", {
		enumerable: !0,
		get: function() {
			return f.decodeHTMLAttribute;
		}
	}), Object.defineProperty(e, "decodeHTML4", {
		enumerable: !0,
		get: function() {
			return f.decodeHTML;
		}
	}), Object.defineProperty(e, "decodeHTML5", {
		enumerable: !0,
		get: function() {
			return f.decodeHTML;
		}
	}), Object.defineProperty(e, "decodeHTML4Strict", {
		enumerable: !0,
		get: function() {
			return f.decodeHTMLStrict;
		}
	}), Object.defineProperty(e, "decodeHTML5Strict", {
		enumerable: !0,
		get: function() {
			return f.decodeHTMLStrict;
		}
	}), Object.defineProperty(e, "decodeXMLStrict", {
		enumerable: !0,
		get: function() {
			return f.decodeXML;
		}
	});
})), g = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.attributeNames = e.elementNames = void 0, e.elementNames = new Map(`altGlyph.altGlyphDef.altGlyphItem.animateColor.animateMotion.animateTransform.clipPath.feBlend.feColorMatrix.feComponentTransfer.feComposite.feConvolveMatrix.feDiffuseLighting.feDisplacementMap.feDistantLight.feDropShadow.feFlood.feFuncA.feFuncB.feFuncG.feFuncR.feGaussianBlur.feImage.feMerge.feMergeNode.feMorphology.feOffset.fePointLight.feSpecularLighting.feSpotLight.feTile.feTurbulence.foreignObject.glyphRef.linearGradient.radialGradient.textPath`.split(`.`).map(function(e) {
		return [e.toLowerCase(), e];
	})), e.attributeNames = new Map(`definitionURL.attributeName.attributeType.baseFrequency.baseProfile.calcMode.clipPathUnits.diffuseConstant.edgeMode.filterUnits.glyphRef.gradientTransform.gradientUnits.kernelMatrix.kernelUnitLength.keyPoints.keySplines.keyTimes.lengthAdjust.limitingConeAngle.markerHeight.markerUnits.markerWidth.maskContentUnits.maskUnits.numOctaves.pathLength.patternContentUnits.patternTransform.patternUnits.pointsAtX.pointsAtY.pointsAtZ.preserveAlpha.preserveAspectRatio.primitiveUnits.refX.refY.repeatCount.repeatDur.requiredExtensions.requiredFeatures.specularConstant.specularExponent.spreadMethod.startOffset.stdDeviation.stitchTiles.surfaceScale.systemLanguage.tableValues.targetX.targetY.textLength.viewBox.viewTarget.xChannelSelector.yChannelSelector.zoomAndPan`.split(`.`).map(function(e) {
		return [e.toLowerCase(), e];
	}));
})), _ = e(((e) => {
	var t = e && e.__assign || function() {
		return t = Object.assign || function(e) {
			for (var t, n = 1, r = arguments.length; n < r; n++) for (var i in t = arguments[n], t) Object.prototype.hasOwnProperty.call(t, i) && (e[i] = t[i]);
			return e;
		}, t.apply(this, arguments);
	}, n = e && e.__createBinding || (Object.create ? (function(e, t, n, r) {
		r === void 0 && (r = n);
		var i = Object.getOwnPropertyDescriptor(t, n);
		(!i || (`get` in i ? !t.__esModule : i.writable || i.configurable)) && (i = {
			enumerable: !0,
			get: function() {
				return t[n];
			}
		}), Object.defineProperty(e, r, i);
	}) : (function(e, t, n, r) {
		r === void 0 && (r = n), e[r] = t[n];
	})), r = e && e.__setModuleDefault || (Object.create ? (function(e, t) {
		Object.defineProperty(e, "default", {
			enumerable: !0,
			value: t
		});
	}) : function(e, t) {
		e.default = t;
	}), i = e && e.__importStar || function(e) {
		if (e && e.__esModule) return e;
		var t = {};
		if (e != null) for (var i in e) i !== "default" && Object.prototype.hasOwnProperty.call(e, i) && n(t, e, i);
		return r(t, e), t;
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.render = void 0;
	var o = i(a()), s = h(), c = g(), l = /* @__PURE__ */ new Set([
		`style`,
		`script`,
		`xmp`,
		`iframe`,
		`noembed`,
		`noframes`,
		`plaintext`,
		`noscript`
	]);
	function u(e) {
		return e.replace(/"/g, `&quot;`);
	}
	function d(e, t) {
		if (e) {
			var n = (t.encodeEntities ?? t.decodeEntities) === !1 ? u : t.xmlMode || t.encodeEntities !== `utf8` ? s.encodeXML : s.escapeAttribute;
			return Object.keys(e).map(function(r) {
				var i = e[r] ?? ``;
				return t.xmlMode === `foreign` && (r = c.attributeNames.get(r) ?? r), !t.emptyAttrs && !t.xmlMode && i === `` ? r : `${r}="${n(i)}"`;
			}).join(` `);
		}
	}
	var f = /* @__PURE__ */ new Set([
		`area`,
		`base`,
		`basefont`,
		`br`,
		`col`,
		`command`,
		`embed`,
		`frame`,
		`hr`,
		`img`,
		`input`,
		`isindex`,
		`keygen`,
		`link`,
		`meta`,
		`param`,
		`source`,
		`track`,
		`wbr`
	]);
	function p(e, t) {
		t === void 0 && (t = {});
		for (var n = (`length` in e) ? e : [e], r = ``, i = 0; i < n.length; i++) r += m(n[i], t);
		return r;
	}
	e.render = p, e.default = p;
	function m(e, t) {
		switch (e.type) {
			case o.Root: return p(e.children, t);
			case o.Doctype:
			case o.Directive: return b(e);
			case o.Comment: return C(e);
			case o.CDATA: return S(e);
			case o.Script:
			case o.Style:
			case o.Tag: return y(e, t);
			case o.Text: return x(e, t);
		}
	}
	var _ = /* @__PURE__ */ new Set([
		`mi`,
		`mo`,
		`mn`,
		`ms`,
		`mtext`,
		`annotation-xml`,
		`foreignObject`,
		`desc`,
		`title`
	]), v = /* @__PURE__ */ new Set([`svg`, `math`]);
	function y(e, n) {
		n.xmlMode === `foreign` && (e.name = c.elementNames.get(e.name) ?? e.name, e.parent && _.has(e.parent.name) && (n = t(t({}, n), { xmlMode: !1 }))), !n.xmlMode && v.has(e.name) && (n = t(t({}, n), { xmlMode: `foreign` }));
		var r = `<${e.name}`, i = d(e.attribs, n);
		return i && (r += ` ${i}`), e.children.length === 0 && (n.xmlMode ? n.selfClosingTags !== !1 : n.selfClosingTags && f.has(e.name)) ? (n.xmlMode || (r += ` `), r += `/>`) : (r += `>`, e.children.length > 0 && (r += p(e.children, n)), (n.xmlMode || !f.has(e.name)) && (r += `</${e.name}>`)), r;
	}
	function b(e) {
		return `<${e.data}>`;
	}
	function x(e, t) {
		var n = e.data || ``;
		return (t.encodeEntities ?? t.decodeEntities) !== !1 && !(!t.xmlMode && e.parent && l.has(e.parent.name)) && (n = t.xmlMode || t.encodeEntities !== `utf8` ? (0, s.encodeXML)(n) : (0, s.escapeText)(n)), n;
	}
	function S(e) {
		return `<![CDATA[${e.children[0].data}]]>`;
	}
	function C(e) {
		return `<!--${e.data}-->`;
	}
})), v = e(((e) => {
	var t = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.getOuterHTML = o, e.getInnerHTML = c, e.getText = l, e.textContent = u, e.innerText = d;
	var n = s(), r = t(_()), i = a();
	function o(e, t) {
		return (0, r.default)(e, t);
	}
	function c(e, t) {
		return (0, n.hasChildren)(e) ? e.children.map(function(e) {
			return o(e, t);
		}).join(``) : ``;
	}
	function l(e) {
		return Array.isArray(e) ? e.map(l).join(``) : (0, n.isTag)(e) ? e.name === `br` ? `
` : l(e.children) : (0, n.isCDATA)(e) ? l(e.children) : (0, n.isText)(e) ? e.data : ``;
	}
	function u(e) {
		return Array.isArray(e) ? e.map(u).join(``) : (0, n.hasChildren)(e) && !(0, n.isComment)(e) ? u(e.children) : (0, n.isText)(e) ? e.data : ``;
	}
	function d(e) {
		return Array.isArray(e) ? e.map(d).join(``) : (0, n.hasChildren)(e) && (e.type === i.ElementType.Tag || (0, n.isCDATA)(e)) ? d(e.children) : (0, n.isText)(e) ? e.data : ``;
	}
})), y = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.getChildren = n, e.getParent = r, e.getSiblings = i, e.getAttributeValue = a, e.hasAttrib = o, e.getName = c, e.nextElementSibling = l, e.prevElementSibling = u;
	var t = s();
	function n(e) {
		return (0, t.hasChildren)(e) ? e.children : [];
	}
	function r(e) {
		return e.parent || null;
	}
	function i(e) {
		var t, i, a = r(e);
		if (a != null) return n(a);
		for (var o = [e], s = e.prev, c = e.next; s != null;) o.unshift(s), t = s, s = t.prev;
		for (; c != null;) o.push(c), i = c, c = i.next;
		return o;
	}
	function a(e, t) {
		return e.attribs?.[t];
	}
	function o(e, t) {
		return e.attribs != null && Object.prototype.hasOwnProperty.call(e.attribs, t) && e.attribs[t] != null;
	}
	function c(e) {
		return e.name;
	}
	function l(e) {
		for (var n, r = e.next; r !== null && !(0, t.isTag)(r);) n = r, r = n.next;
		return r;
	}
	function u(e) {
		for (var n, r = e.prev; r !== null && !(0, t.isTag)(r);) n = r, r = n.prev;
		return r;
	}
})), b = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.removeElement = t, e.replaceElement = n, e.appendChild = r, e.append = i, e.prependChild = a, e.prepend = o;
	function t(e) {
		if (e.prev && (e.prev.next = e.next), e.next && (e.next.prev = e.prev), e.parent) {
			var t = e.parent.children, n = t.lastIndexOf(e);
			n >= 0 && t.splice(n, 1);
		}
		e.next = null, e.prev = null, e.parent = null;
	}
	function n(e, t) {
		var n = t.prev = e.prev;
		n && (n.next = t);
		var r = t.next = e.next;
		r && (r.prev = t);
		var i = t.parent = e.parent;
		if (i) {
			var a = i.children;
			a[a.lastIndexOf(e)] = t, e.parent = null;
		}
	}
	function r(e, n) {
		if (t(n), n.next = null, n.parent = e, e.children.push(n) > 1) {
			var r = e.children[e.children.length - 2];
			r.next = n, n.prev = r;
		} else n.prev = null;
	}
	function i(e, n) {
		t(n);
		var r = e.parent, i = e.next;
		if (n.next = i, n.prev = e, e.next = n, n.parent = r, i) {
			if (i.prev = n, r) {
				var a = r.children;
				a.splice(a.lastIndexOf(i), 0, n);
			}
		} else r && r.children.push(n);
	}
	function a(e, n) {
		if (t(n), n.parent = e, n.prev = null, e.children.unshift(n) !== 1) {
			var r = e.children[1];
			r.prev = n, n.next = r;
		} else n.next = null;
	}
	function o(e, n) {
		t(n);
		var r = e.parent;
		if (r) {
			var i = r.children;
			i.splice(i.indexOf(e), 0, n);
		}
		e.prev && (e.prev.next = n), n.parent = r, n.prev = e.prev, n.next = e, e.prev = n;
	}
})), x = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.filter = n, e.find = r, e.findOneChild = i, e.findOne = a, e.existsOne = o, e.findAll = c;
	var t = s();
	function n(e, t, n, i) {
		return n === void 0 && (n = !0), i === void 0 && (i = Infinity), r(e, Array.isArray(t) ? t : [t], n, i);
	}
	function r(e, n, r, i) {
		for (var a = [], o = [Array.isArray(n) ? n : [n]], s = [0];;) {
			if (s[0] >= o[0].length) {
				if (s.length === 1) return a;
				o.shift(), s.shift();
				continue;
			}
			var c = o[0][s[0]++];
			if (e(c) && (a.push(c), --i <= 0)) return a;
			r && (0, t.hasChildren)(c) && c.children.length > 0 && (s.unshift(0), o.unshift(c.children));
		}
	}
	function i(e, t) {
		return t.find(e);
	}
	function a(e, n, r) {
		r === void 0 && (r = !0);
		for (var i = Array.isArray(n) ? n : [n], o = 0; o < i.length; o++) {
			var s = i[o];
			if ((0, t.isTag)(s) && e(s)) return s;
			if (r && (0, t.hasChildren)(s) && s.children.length > 0) {
				var c = a(e, s.children, !0);
				if (c) return c;
			}
		}
		return null;
	}
	function o(e, n) {
		return (Array.isArray(n) ? n : [n]).some(function(n) {
			return (0, t.isTag)(n) && e(n) || (0, t.hasChildren)(n) && o(e, n.children);
		});
	}
	function c(e, n) {
		for (var r = [], i = [Array.isArray(n) ? n : [n]], a = [0];;) {
			if (a[0] >= i[0].length) {
				if (i.length === 1) return r;
				i.shift(), a.shift();
				continue;
			}
			var o = i[0][a[0]++];
			(0, t.isTag)(o) && e(o) && r.push(o), (0, t.hasChildren)(o) && o.children.length > 0 && (a.unshift(0), i.unshift(o.children));
		}
	}
})), S = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.testElement = c, e.getElements = l, e.getElementById = u, e.getElementsByTagName = d, e.getElementsByClassName = f, e.getElementsByTagType = p;
	var t = s(), n = x(), r = {
		tag_name: function(e) {
			return typeof e == `function` ? function(n) {
				return (0, t.isTag)(n) && e(n.name);
			} : e === `*` ? t.isTag : function(n) {
				return (0, t.isTag)(n) && n.name === e;
			};
		},
		tag_type: function(e) {
			return typeof e == `function` ? function(t) {
				return e(t.type);
			} : function(t) {
				return t.type === e;
			};
		},
		tag_contains: function(e) {
			return typeof e == `function` ? function(n) {
				return (0, t.isText)(n) && e(n.data);
			} : function(n) {
				return (0, t.isText)(n) && n.data === e;
			};
		}
	};
	function i(e, n) {
		return typeof n == `function` ? function(r) {
			return (0, t.isTag)(r) && n(r.attribs[e]);
		} : function(r) {
			return (0, t.isTag)(r) && r.attribs[e] === n;
		};
	}
	function a(e, t) {
		return function(n) {
			return e(n) || t(n);
		};
	}
	function o(e) {
		var t = Object.keys(e).map(function(t) {
			var n = e[t];
			return Object.prototype.hasOwnProperty.call(r, t) ? r[t](n) : i(t, n);
		});
		return t.length === 0 ? null : t.reduce(a);
	}
	function c(e, t) {
		var n = o(e);
		return !n || n(t);
	}
	function l(e, t, r, i) {
		i === void 0 && (i = Infinity);
		var a = o(e);
		return a ? (0, n.filter)(a, t, r, i) : [];
	}
	function u(e, t, r) {
		return r === void 0 && (r = !0), Array.isArray(t) || (t = [t]), (0, n.findOne)(i(`id`, e), t, r);
	}
	function d(e, t, i, a) {
		return i === void 0 && (i = !0), a === void 0 && (a = Infinity), (0, n.filter)(r.tag_name(e), t, i, a);
	}
	function f(e, t, r, a) {
		return r === void 0 && (r = !0), a === void 0 && (a = Infinity), (0, n.filter)(i(`class`, e), t, r, a);
	}
	function p(e, t, i, a) {
		return i === void 0 && (i = !0), a === void 0 && (a = Infinity), (0, n.filter)(r.tag_type(e), t, i, a);
	}
})), C = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.DocumentPosition = void 0, e.removeSubsets = n, e.compareDocumentPosition = i, e.uniqueSort = a;
	var t = s();
	function n(e) {
		for (var t = e.length; --t >= 0;) {
			var n = e[t];
			if (t > 0 && e.lastIndexOf(n, t - 1) >= 0) {
				e.splice(t, 1);
				continue;
			}
			for (var r = n.parent; r; r = r.parent) if (e.includes(r)) {
				e.splice(t, 1);
				break;
			}
		}
		return e;
	}
	var r;
	(function(e) {
		e[e.DISCONNECTED = 1] = `DISCONNECTED`, e[e.PRECEDING = 2] = `PRECEDING`, e[e.FOLLOWING = 4] = `FOLLOWING`, e[e.CONTAINS = 8] = `CONTAINS`, e[e.CONTAINED_BY = 16] = `CONTAINED_BY`;
	})(r || (e.DocumentPosition = r = {}));
	function i(e, n) {
		var i = [], a = [];
		if (e === n) return 0;
		for (var o = (0, t.hasChildren)(e) ? e : e.parent; o;) i.unshift(o), o = o.parent;
		for (o = (0, t.hasChildren)(n) ? n : n.parent; o;) a.unshift(o), o = o.parent;
		for (var s = Math.min(i.length, a.length), c = 0; c < s && i[c] === a[c];) c++;
		if (c === 0) return r.DISCONNECTED;
		var l = i[c - 1], u = l.children, d = i[c], f = a[c];
		return u.indexOf(d) > u.indexOf(f) ? l === n ? r.FOLLOWING | r.CONTAINED_BY : r.FOLLOWING : l === e ? r.PRECEDING | r.CONTAINS : r.PRECEDING;
	}
	function a(e) {
		return e = e.filter(function(e, t, n) {
			return !n.includes(e, t + 1);
		}), e.sort(function(e, t) {
			var n = i(e, t);
			return n & r.PRECEDING ? -1 : n & r.FOLLOWING ? 1 : 0;
		}), e;
	}
})), w = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.getFeed = r;
	var t = v(), n = S();
	function r(e) {
		var t = l(f, e);
		return t ? t.name === `feed` ? i(t) : a(t) : null;
	}
	function i(e) {
		var t = e.children, r = {
			type: `atom`,
			items: (0, n.getElementsByTagName)(`entry`, t).map(function(e) {
				var t = e.children, n = { media: c(t) };
				d(n, `id`, `id`, t), d(n, `title`, `title`, t);
				var r = l(`link`, t)?.attribs.href;
				r && (n.link = r);
				var i = u(`summary`, t) || u(`content`, t);
				i && (n.description = i);
				var a = u(`updated`, t);
				return a && (n.pubDate = new Date(a)), n;
			})
		};
		d(r, `id`, `id`, t), d(r, `title`, `title`, t);
		var i = l(`link`, t)?.attribs.href;
		i && (r.link = i), d(r, `description`, `subtitle`, t);
		var a = u(`updated`, t);
		return a && (r.updated = new Date(a)), d(r, `author`, `email`, t, !0), r;
	}
	function a(e) {
		var t = l(`channel`, e.children)?.children ?? [], r = {
			type: e.name.substr(0, 3),
			id: ``,
			items: (0, n.getElementsByTagName)(`item`, e.children).map(function(e) {
				var t = e.children, n = { media: c(t) };
				d(n, `id`, `guid`, t), d(n, `title`, `title`, t), d(n, `link`, `link`, t), d(n, `description`, `description`, t);
				var r = u(`pubDate`, t) || u(`dc:date`, t);
				return r && (n.pubDate = new Date(r)), n;
			})
		};
		d(r, `title`, `title`, t), d(r, `link`, `link`, t), d(r, `description`, `description`, t);
		var i = u(`lastBuildDate`, t);
		return i && (r.updated = new Date(i)), d(r, `author`, `managingEditor`, t, !0), r;
	}
	var o = [
		`url`,
		`type`,
		`lang`
	], s = [
		`fileSize`,
		`bitrate`,
		`framerate`,
		`samplingrate`,
		`channels`,
		`duration`,
		`height`,
		`width`
	];
	function c(e) {
		return (0, n.getElementsByTagName)(`media:content`, e).map(function(e) {
			for (var t = e.attribs, n = {
				medium: t.medium,
				isDefault: !!t.isDefault
			}, r = 0, i = o; r < i.length; r++) {
				var a = i[r];
				t[a] && (n[a] = t[a]);
			}
			for (var c = 0, l = s; c < l.length; c++) {
				var a = l[c];
				t[a] && (n[a] = parseInt(t[a], 10));
			}
			return t.expression && (n.expression = t.expression), n;
		});
	}
	function l(e, t) {
		return (0, n.getElementsByTagName)(e, t, !0, 1)[0];
	}
	function u(e, r, i) {
		return i === void 0 && (i = !1), (0, t.textContent)((0, n.getElementsByTagName)(e, r, i, 1)).trim();
	}
	function d(e, t, n, r, i) {
		i === void 0 && (i = !1);
		var a = u(n, r, i);
		a && (e[t] = a);
	}
	function f(e) {
		return e === `rss` || e === `feed` || e === `rdf:RDF`;
	}
})), T = e(((e) => {
	var t = e && e.__createBinding || (Object.create ? (function(e, t, n, r) {
		r === void 0 && (r = n);
		var i = Object.getOwnPropertyDescriptor(t, n);
		(!i || (`get` in i ? !t.__esModule : i.writable || i.configurable)) && (i = {
			enumerable: !0,
			get: function() {
				return t[n];
			}
		}), Object.defineProperty(e, r, i);
	}) : (function(e, t, n, r) {
		r === void 0 && (r = n), e[r] = t[n];
	})), n = e && e.__exportStar || function(e, n) {
		for (var r in e) r !== "default" && !Object.prototype.hasOwnProperty.call(n, r) && t(n, e, r);
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.hasChildren = e.isDocument = e.isComment = e.isText = e.isCDATA = e.isTag = void 0, n(v(), e), n(y(), e), n(b(), e), n(x(), e), n(S(), e), n(C(), e), n(w(), e);
	var r = s();
	Object.defineProperty(e, "isTag", {
		enumerable: !0,
		get: function() {
			return r.isTag;
		}
	}), Object.defineProperty(e, "isCDATA", {
		enumerable: !0,
		get: function() {
			return r.isCDATA;
		}
	}), Object.defineProperty(e, "isText", {
		enumerable: !0,
		get: function() {
			return r.isText;
		}
	}), Object.defineProperty(e, "isComment", {
		enumerable: !0,
		get: function() {
			return r.isComment;
		}
	}), Object.defineProperty(e, "isDocument", {
		enumerable: !0,
		get: function() {
			return r.isDocument;
		}
	}), Object.defineProperty(e, "hasChildren", {
		enumerable: !0,
		get: function() {
			return r.hasChildren;
		}
	});
})), E, D, O, k = t((() => {
	(function(e) {
		e.Attribute = `attribute`, e.Pseudo = `pseudo`, e.PseudoElement = `pseudo-element`, e.Tag = `tag`, e.Universal = `universal`, e.Adjacent = `adjacent`, e.Child = `child`, e.Descendant = `descendant`, e.Parent = `parent`, e.Sibling = `sibling`, e.ColumnCombinator = `column-combinator`;
	})(E ||= {}), D = {
		Unknown: null,
		QuirksMode: `quirks`,
		IgnoreCase: !0,
		CaseSensitive: !1
	}, (function(e) {
		e.Any = `any`, e.Element = `element`, e.End = `end`, e.Equals = `equals`, e.Exists = `exists`, e.Hyphen = `hyphen`, e.Not = `not`, e.Start = `start`;
	})(O ||= {});
}));
function A(e) {
	switch (e.type) {
		case E.Adjacent:
		case E.Child:
		case E.Descendant:
		case E.Parent:
		case E.Sibling:
		case E.ColumnCombinator: return !0;
		default: return !1;
	}
}
function ee(e, t, n) {
	let r = parseInt(t, 16) - 65536;
	return r !== r || n ? t : r < 0 ? String.fromCharCode(r + 65536) : String.fromCharCode(r >> 10 | 55296, r & 1023 | 56320);
}
function j(e) {
	return e.replace(I, ee);
}
function M(e) {
	return e === 39 || e === 34;
}
function N(e) {
	return e === 32 || e === 9 || e === 10 || e === 12 || e === 13;
}
function te(e) {
	let t = [], n = P(t, `${e}`, 0);
	if (n < e.length) throw Error(`Unmatched selector: ${e.slice(n)}`);
	return t;
}
function P(e, t, n) {
	let r = [];
	function i(e) {
		let r = t.slice(n + e).match(F);
		if (!r) throw Error(`Expected name, found ${t.slice(n)}`);
		let [i] = r;
		return n += e + i.length, j(i);
	}
	function a(e) {
		for (n += e; n < t.length && N(t.charCodeAt(n));) n++;
	}
	function o() {
		n += 1;
		let e = n, r = 1;
		for (; r > 0 && n < t.length; n++) t.charCodeAt(n) === 40 && !s(n) ? r++ : t.charCodeAt(n) === 41 && !s(n) && r--;
		if (r) throw Error(`Parenthesis not matched`);
		return j(t.slice(e, n - 1));
	}
	function s(e) {
		let n = 0;
		for (; t.charCodeAt(--e) === 92;) n++;
		return (n & 1) == 1;
	}
	function c() {
		if (r.length > 0 && A(r[r.length - 1])) throw Error(`Did not expect successive traversals.`);
	}
	function l(e) {
		if (r.length > 0 && r[r.length - 1].type === E.Descendant) {
			r[r.length - 1].type = e;
			return;
		}
		c(), r.push({ type: e });
	}
	function u(e, t) {
		r.push({
			type: E.Attribute,
			name: e,
			action: t,
			value: i(1),
			namespace: null,
			ignoreCase: `quirks`
		});
	}
	function d() {
		if (r.length && r[r.length - 1].type === E.Descendant && r.pop(), r.length === 0) throw Error(`Empty sub-selector`);
		e.push(r);
	}
	if (a(0), t.length === n) return n;
	loop: for (; n < t.length;) {
		let e = t.charCodeAt(n);
		switch (e) {
			case 32:
			case 9:
			case 10:
			case 12:
			case 13:
				(r.length === 0 || r[0].type !== E.Descendant) && (c(), r.push({ type: E.Descendant })), a(1);
				break;
			case 62:
				l(E.Child), a(1);
				break;
			case 60:
				l(E.Parent), a(1);
				break;
			case 126:
				l(E.Sibling), a(1);
				break;
			case 43:
				l(E.Adjacent), a(1);
				break;
			case 46:
				u(`class`, O.Element);
				break;
			case 35:
				u(`id`, O.Equals);
				break;
			case 91: {
				a(1);
				let e, o = null;
				t.charCodeAt(n) === 124 ? e = i(1) : t.startsWith(`*|`, n) ? (o = `*`, e = i(2)) : (e = i(0), t.charCodeAt(n) === 124 && t.charCodeAt(n + 1) !== 61 && (o = e, e = i(1))), a(0);
				let c = O.Exists, l = L.get(t.charCodeAt(n));
				if (l) {
					if (c = l, t.charCodeAt(n + 1) !== 61) throw Error("Expected `=`");
					a(2);
				} else t.charCodeAt(n) === 61 && (c = O.Equals, a(1));
				let u = ``, d = null;
				if (c !== `exists`) {
					if (M(t.charCodeAt(n))) {
						let e = t.charCodeAt(n), r = n + 1;
						for (; r < t.length && (t.charCodeAt(r) !== e || s(r));) r += 1;
						if (t.charCodeAt(r) !== e) throw Error(`Attribute value didn't end`);
						u = j(t.slice(n + 1, r)), n = r + 1;
					} else {
						let e = n;
						for (; n < t.length && (!N(t.charCodeAt(n)) && t.charCodeAt(n) !== 93 || s(n));) n += 1;
						u = j(t.slice(e, n));
					}
					a(0);
					let e = t.charCodeAt(n) | 32;
					e === 115 ? (d = !1, a(1)) : e === 105 && (d = !0, a(1));
				}
				if (t.charCodeAt(n) !== 93) throw Error(`Attribute selector didn't terminate`);
				n += 1;
				let f = {
					type: E.Attribute,
					name: e,
					action: c,
					value: u,
					namespace: o,
					ignoreCase: d
				};
				r.push(f);
				break;
			}
			case 58: {
				if (t.charCodeAt(n + 1) === 58) {
					r.push({
						type: E.PseudoElement,
						name: i(2).toLowerCase(),
						data: t.charCodeAt(n) === 40 ? o() : null
					});
					continue;
				}
				let e = i(1).toLowerCase(), a = null;
				if (t.charCodeAt(n) === 40) if (R.has(e)) {
					if (M(t.charCodeAt(n + 1))) throw Error(`Pseudo-selector ${e} cannot be quoted`);
					if (a = [], n = P(a, t, n + 1), t.charCodeAt(n) !== 41) throw Error(`Missing closing parenthesis in :${e} (${t})`);
					n += 1;
				} else {
					if (a = o(), z.has(e)) {
						let e = a.charCodeAt(0);
						e === a.charCodeAt(a.length - 1) && M(e) && (a = a.slice(1, -1));
					}
					a = j(a);
				}
				r.push({
					type: E.Pseudo,
					name: e,
					data: a
				});
				break;
			}
			case 44:
				d(), r = [], a(1);
				break;
			default: {
				if (t.startsWith(`/*`, n)) {
					let e = t.indexOf(`*/`, n + 2);
					if (e < 0) throw Error(`Comment was not terminated`);
					n = e + 2, r.length === 0 && a(0);
					break;
				}
				let o = null, s;
				if (e === 42) n += 1, s = `*`;
				else if (e === 124) {
					if (s = ``, t.charCodeAt(n + 1) === 124) {
						l(E.ColumnCombinator), a(2);
						break;
					}
				} else if (F.test(t.slice(n))) s = i(0);
				else break loop;
				t.charCodeAt(n) === 124 && t.charCodeAt(n + 1) !== 124 && (o = s, t.charCodeAt(n + 1) === 42 ? (s = `*`, n += 2) : s = i(1)), r.push(s === `*` ? {
					type: E.Universal,
					namespace: o
				} : {
					type: E.Tag,
					name: s,
					namespace: o
				});
			}
		}
	}
	return d(), n;
}
var F, I, L, R, z, ne = t((() => {
	k(), F = /^[^\\#]?(?:\\(?:[\da-f]{1,6}\s?|.)|[\w\-\u00b0-\uFFFF])+/, I = /\\([\da-f]{1,6}\s?|(\s)|.)/gi, L = /* @__PURE__ */ new Map([
		[126, O.Element],
		[94, O.Start],
		[36, O.End],
		[42, O.Any],
		[33, O.Not],
		[124, O.Hyphen]
	]), R = /* @__PURE__ */ new Set([
		`has`,
		`not`,
		`matches`,
		`is`,
		`where`,
		`host`,
		`host-context`
	]), z = /* @__PURE__ */ new Set([`contains`, `icontains`]);
}));
function B(e) {
	return e.map((e) => e.map(re).join(``)).join(`, `);
}
function re(e, t, n) {
	switch (e.type) {
		case E.Child: return t === 0 ? `> ` : ` > `;
		case E.Parent: return t === 0 ? `< ` : ` < `;
		case E.Sibling: return t === 0 ? `~ ` : ` ~ `;
		case E.Adjacent: return t === 0 ? `+ ` : ` + `;
		case E.Descendant: return ` `;
		case E.ColumnCombinator: return t === 0 ? `|| ` : ` || `;
		case E.Universal: return e.namespace === `*` && t + 1 < n.length && `name` in n[t + 1] ? `` : `${H(e.namespace)}*`;
		case E.Tag: return V(e);
		case E.PseudoElement: return `::${U(e.name, J)}${e.data === null ? `` : `(${U(e.data, q)})`}`;
		case E.Pseudo: return `:${U(e.name, J)}${e.data === null ? `` : `(${typeof e.data == `string` ? U(e.data, q) : B(e.data)})`}`;
		case E.Attribute: {
			if (e.name === `id` && e.action === O.Equals && e.ignoreCase === `quirks` && !e.namespace) return `#${U(e.value, J)}`;
			if (e.name === `class` && e.action === O.Element && e.ignoreCase === `quirks` && !e.namespace) return `.${U(e.value, J)}`;
			let t = V(e);
			return e.action === O.Exists ? `[${t}]` : `[${t}${ie(e.action)}="${U(e.value, K)}"${e.ignoreCase === null ? `` : e.ignoreCase ? ` i` : ` s`}]`;
		}
	}
}
function ie(e) {
	switch (e) {
		case O.Equals: return ``;
		case O.Element: return `~`;
		case O.Start: return `^`;
		case O.End: return `$`;
		case O.Any: return `*`;
		case O.Not: return `!`;
		case O.Hyphen: return `|`;
		case O.Exists: throw Error(`Shouldn't be here`);
	}
}
function V(e) {
	return `${H(e.namespace)}${U(e.name, J)}`;
}
function H(e) {
	return e === null ? `` : `${e === `*` ? `*` : U(e, J)}|`;
}
function U(e, t) {
	let n = 0, r = ``;
	for (let i = 0; i < e.length; i++) t.has(e.charCodeAt(i)) && (r += `${e.slice(n, i)}\\${e.charAt(i)}`, n = i + 1);
	return r.length > 0 ? r + e.slice(n) : e;
}
var W, G, K, q, J, ae = t((() => {
	k(), W = [`\\`, `"`], G = [
		...W,
		`(`,
		`)`
	], K = new Set(W.map((e) => e.charCodeAt(0))), q = new Set(G.map((e) => e.charCodeAt(0))), J = new Set([
		...G,
		`~`,
		`^`,
		`$`,
		`*`,
		`+`,
		`!`,
		`|`,
		`:`,
		`[`,
		`]`,
		` `,
		`.`
	].map((e) => e.charCodeAt(0)));
})), Y = n({
	AttributeAction: () => O,
	IgnoreCaseMode: () => D,
	SelectorType: () => E,
	isTraversal: () => A,
	parse: () => te,
	stringify: () => B
}), X = t((() => {
	k(), ne(), ae();
})), Z = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.isTraversal = void 0;
	var t = (X(), r(Y)), n = /* @__PURE__ */ new Map([
		[t.SelectorType.Universal, 50],
		[t.SelectorType.Tag, 30],
		[t.SelectorType.Attribute, 1],
		[t.SelectorType.Pseudo, 0]
	]);
	function i(e) {
		return !n.has(e.type);
	}
	e.isTraversal = i;
	var a = /* @__PURE__ */ new Map([
		[t.AttributeAction.Exists, 10],
		[t.AttributeAction.Equals, 8],
		[t.AttributeAction.Not, 7],
		[t.AttributeAction.Start, 6],
		[t.AttributeAction.End, 6],
		[t.AttributeAction.Any, 5]
	]);
	function o(e) {
		for (var t = e.map(s), n = 1; n < e.length; n++) {
			var r = t[n];
			if (!(r < 0)) for (var i = n - 1; i >= 0 && r < t[i]; i--) {
				var a = e[i + 1];
				e[i + 1] = e[i], e[i] = a, t[i + 1] = t[i], t[i] = r;
			}
		}
	}
	e.default = o;
	function s(e) {
		var r = n.get(e.type) ?? -1;
		return e.type === t.SelectorType.Attribute ? (r = a.get(e.action) ?? 4, e.action === t.AttributeAction.Equals && e.name === `id` && (r = 9), e.ignoreCase && (r >>= 1)) : e.type === t.SelectorType.Pseudo && (e.data ? e.name === `has` || e.name === `contains` ? r = 0 : Array.isArray(e.data) ? (r = Math.min.apply(Math, e.data.map(function(e) {
			return Math.min.apply(Math, e.map(s));
		})), r < 0 && (r = 0)) : r = 2 : r = 3), r;
	}
})), oe = e(((e) => {
	var t = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.attributeRules = void 0;
	var n = t(i()), r = /[-[\]{}()*+?.,\\^$|#\s]/g;
	function a(e) {
		return e.replace(r, `\\$&`);
	}
	var o = new Set(`accept.accept-charset.align.alink.axis.bgcolor.charset.checked.clear.codetype.color.compact.declare.defer.dir.direction.disabled.enctype.face.frame.hreflang.http-equiv.lang.language.link.media.method.multiple.nohref.noresize.noshade.nowrap.readonly.rel.rev.rules.scope.scrolling.selected.shape.target.text.type.valign.valuetype.vlink`.split(`.`));
	function s(e, t) {
		return typeof e.ignoreCase == `boolean` ? e.ignoreCase : e.ignoreCase === `quirks` ? !!t.quirksMode : !t.xmlMode && o.has(e.name);
	}
	e.attributeRules = {
		equals: function(e, t, n) {
			var r = n.adapter, i = t.name, a = t.value;
			return s(t, n) ? (a = a.toLowerCase(), function(t) {
				var n = r.getAttributeValue(t, i);
				return n != null && n.length === a.length && n.toLowerCase() === a && e(t);
			}) : function(t) {
				return r.getAttributeValue(t, i) === a && e(t);
			};
		},
		hyphen: function(e, t, n) {
			var r = n.adapter, i = t.name, a = t.value, o = a.length;
			return s(t, n) ? (a = a.toLowerCase(), function(t) {
				var n = r.getAttributeValue(t, i);
				return n != null && (n.length === o || n.charAt(o) === `-`) && n.substr(0, o).toLowerCase() === a && e(t);
			}) : function(t) {
				var n = r.getAttributeValue(t, i);
				return n != null && (n.length === o || n.charAt(o) === `-`) && n.substr(0, o) === a && e(t);
			};
		},
		element: function(e, t, r) {
			var i = r.adapter, o = t.name, c = t.value;
			if (/\s/.test(c)) return n.default.falseFunc;
			var l = RegExp(`(?:^|\\s)${a(c)}(?:\$|\\s)`, s(t, r) ? `i` : ``);
			return function(t) {
				var n = i.getAttributeValue(t, o);
				return n != null && n.length >= c.length && l.test(n) && e(t);
			};
		},
		exists: function(e, t, n) {
			var r = t.name, i = n.adapter;
			return function(t) {
				return i.hasAttrib(t, r) && e(t);
			};
		},
		start: function(e, t, r) {
			var i = r.adapter, a = t.name, o = t.value, c = o.length;
			return c === 0 ? n.default.falseFunc : s(t, r) ? (o = o.toLowerCase(), function(t) {
				var n = i.getAttributeValue(t, a);
				return n != null && n.length >= c && n.substr(0, c).toLowerCase() === o && e(t);
			}) : function(t) {
				return !!i.getAttributeValue(t, a)?.startsWith(o) && e(t);
			};
		},
		end: function(e, t, r) {
			var i = r.adapter, a = t.name, o = t.value, c = -o.length;
			return c === 0 ? n.default.falseFunc : s(t, r) ? (o = o.toLowerCase(), function(t) {
				return i.getAttributeValue(t, a)?.substr(c).toLowerCase() === o && e(t);
			}) : function(t) {
				return !!i.getAttributeValue(t, a)?.endsWith(o) && e(t);
			};
		},
		any: function(e, t, r) {
			var i = r.adapter, o = t.name, c = t.value;
			if (c === ``) return n.default.falseFunc;
			if (s(t, r)) {
				var l = new RegExp(a(c), `i`);
				return function(t) {
					var n = i.getAttributeValue(t, o);
					return n != null && n.length >= c.length && l.test(n) && e(t);
				};
			}
			return function(t) {
				return !!i.getAttributeValue(t, o)?.includes(c) && e(t);
			};
		},
		not: function(e, t, n) {
			var r = n.adapter, i = t.name, a = t.value;
			return a === `` ? function(t) {
				return !!r.getAttributeValue(t, i) && e(t);
			} : s(t, n) ? (a = a.toLowerCase(), function(t) {
				var n = r.getAttributeValue(t, i);
				return (n == null || n.length !== a.length || n.toLowerCase() !== a) && e(t);
			}) : function(t) {
				return r.getAttributeValue(t, i) !== a && e(t);
			};
		}
	};
})), se = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.parse = void 0;
	var t = /* @__PURE__ */ new Set([
		9,
		10,
		12,
		13,
		32
	]), n = 48, r = 57;
	function i(e) {
		if (e = e.trim().toLowerCase(), e === `even`) return [2, 0];
		if (e === `odd`) return [2, 1];
		var i = 0, a = 0, o = c(), s = l();
		if (i < e.length && e.charAt(i) === `n` && (i++, a = o * (s ?? 1), u(), i < e.length ? (o = c(), u(), s = l()) : o = s = 0), s === null || i < e.length) throw Error(`n-th rule couldn't be parsed ('${e}')`);
		return [a, o * s];
		function c() {
			return e.charAt(i) === `-` ? (i++, -1) : (e.charAt(i) === `+` && i++, 1);
		}
		function l() {
			for (var t = i, a = 0; i < e.length && e.charCodeAt(i) >= n && e.charCodeAt(i) <= r;) a = a * 10 + (e.charCodeAt(i) - n), i++;
			return i === t ? null : a;
		}
		function u() {
			for (; i < e.length && t.has(e.charCodeAt(i));) i++;
		}
	}
	e.parse = i;
})), ce = e(((e) => {
	var t = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.generate = e.compile = void 0;
	var n = t(i());
	function r(e) {
		var t = e[0], r = e[1] - 1;
		if (r < 0 && t <= 0) return n.default.falseFunc;
		if (t === -1) return function(e) {
			return e <= r;
		};
		if (t === 0) return function(e) {
			return e === r;
		};
		if (t === 1) return r < 0 ? n.default.trueFunc : function(e) {
			return e >= r;
		};
		var i = Math.abs(t), a = (r % i + i) % i;
		return t > 1 ? function(e) {
			return e >= r && e % i === a;
		} : function(e) {
			return e <= r && e % i === a;
		};
	}
	e.compile = r;
	function a(e) {
		var t = e[0], n = e[1] - 1, r = 0;
		if (t < 0) {
			var i = -t, a = (n % i + i) % i;
			return function() {
				var e = a + i * r++;
				return e > n ? null : e;
			};
		}
		return t === 0 ? n < 0 ? function() {
			return null;
		} : function() {
			return r++ === 0 ? n : null;
		} : (n < 0 && (n += t * Math.ceil(-n / t)), function() {
			return t * r++ + n;
		});
	}
	e.generate = a;
})), le = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.sequence = e.generate = e.compile = e.parse = void 0;
	var t = se();
	Object.defineProperty(e, "parse", {
		enumerable: !0,
		get: function() {
			return t.parse;
		}
	});
	var n = ce();
	Object.defineProperty(e, "compile", {
		enumerable: !0,
		get: function() {
			return n.compile;
		}
	}), Object.defineProperty(e, "generate", {
		enumerable: !0,
		get: function() {
			return n.generate;
		}
	});
	function r(e) {
		return (0, n.compile)((0, t.parse)(e));
	}
	e.default = r;
	function i(e) {
		return (0, n.generate)((0, t.parse)(e));
	}
	e.sequence = i;
})), ue = e(((e) => {
	var t = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.filters = void 0;
	var n = t(le()), r = t(i());
	function a(e, t) {
		return function(n) {
			var r = t.getParent(n);
			return r != null && t.isTag(r) && e(n);
		};
	}
	e.filters = {
		contains: function(e, t, n) {
			var r = n.adapter;
			return function(n) {
				return e(n) && r.getText(n).includes(t);
			};
		},
		icontains: function(e, t, n) {
			var r = n.adapter, i = t.toLowerCase();
			return function(t) {
				return e(t) && r.getText(t).toLowerCase().includes(i);
			};
		},
		"nth-child": function(e, t, i) {
			var o = i.adapter, s = i.equals, c = (0, n.default)(t);
			return c === r.default.falseFunc ? r.default.falseFunc : c === r.default.trueFunc ? a(e, o) : function(t) {
				for (var n = o.getSiblings(t), r = 0, i = 0; i < n.length && !s(t, n[i]); i++) o.isTag(n[i]) && r++;
				return c(r) && e(t);
			};
		},
		"nth-last-child": function(e, t, i) {
			var o = i.adapter, s = i.equals, c = (0, n.default)(t);
			return c === r.default.falseFunc ? r.default.falseFunc : c === r.default.trueFunc ? a(e, o) : function(t) {
				for (var n = o.getSiblings(t), r = 0, i = n.length - 1; i >= 0 && !s(t, n[i]); i--) o.isTag(n[i]) && r++;
				return c(r) && e(t);
			};
		},
		"nth-of-type": function(e, t, i) {
			var o = i.adapter, s = i.equals, c = (0, n.default)(t);
			return c === r.default.falseFunc ? r.default.falseFunc : c === r.default.trueFunc ? a(e, o) : function(t) {
				for (var n = o.getSiblings(t), r = 0, i = 0; i < n.length; i++) {
					var a = n[i];
					if (s(t, a)) break;
					o.isTag(a) && o.getName(a) === o.getName(t) && r++;
				}
				return c(r) && e(t);
			};
		},
		"nth-last-of-type": function(e, t, i) {
			var o = i.adapter, s = i.equals, c = (0, n.default)(t);
			return c === r.default.falseFunc ? r.default.falseFunc : c === r.default.trueFunc ? a(e, o) : function(t) {
				for (var n = o.getSiblings(t), r = 0, i = n.length - 1; i >= 0; i--) {
					var a = n[i];
					if (s(t, a)) break;
					o.isTag(a) && o.getName(a) === o.getName(t) && r++;
				}
				return c(r) && e(t);
			};
		},
		root: function(e, t, n) {
			var r = n.adapter;
			return function(t) {
				var n = r.getParent(t);
				return (n == null || !r.isTag(n)) && e(t);
			};
		},
		scope: function(t, n, r, i) {
			var a = r.equals;
			return !i || i.length === 0 ? e.filters.root(t, n, r) : i.length === 1 ? function(e) {
				return a(i[0], e) && t(e);
			} : function(e) {
				return i.includes(e) && t(e);
			};
		},
		hover: o(`isHovered`),
		visited: o(`isVisited`),
		active: o(`isActive`)
	};
	function o(e) {
		return function(t, n, i) {
			var a = i.adapter[e];
			return typeof a == `function` ? function(e) {
				return a(e) && t(e);
			} : r.default.falseFunc;
		};
	}
})), de = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.verifyPseudoArgs = e.pseudos = void 0, e.pseudos = {
		empty: function(e, t) {
			var n = t.adapter;
			return !n.getChildren(e).some(function(e) {
				return n.isTag(e) || n.getText(e) !== ``;
			});
		},
		"first-child": function(e, t) {
			var n = t.adapter, r = t.equals;
			if (n.prevElementSibling) return n.prevElementSibling(e) == null;
			var i = n.getSiblings(e).find(function(e) {
				return n.isTag(e);
			});
			return i != null && r(e, i);
		},
		"last-child": function(e, t) {
			for (var n = t.adapter, r = t.equals, i = n.getSiblings(e), a = i.length - 1; a >= 0; a--) {
				if (r(e, i[a])) return !0;
				if (n.isTag(i[a])) break;
			}
			return !1;
		},
		"first-of-type": function(e, t) {
			for (var n = t.adapter, r = t.equals, i = n.getSiblings(e), a = n.getName(e), o = 0; o < i.length; o++) {
				var s = i[o];
				if (r(e, s)) return !0;
				if (n.isTag(s) && n.getName(s) === a) break;
			}
			return !1;
		},
		"last-of-type": function(e, t) {
			for (var n = t.adapter, r = t.equals, i = n.getSiblings(e), a = n.getName(e), o = i.length - 1; o >= 0; o--) {
				var s = i[o];
				if (r(e, s)) return !0;
				if (n.isTag(s) && n.getName(s) === a) break;
			}
			return !1;
		},
		"only-of-type": function(e, t) {
			var n = t.adapter, r = t.equals, i = n.getName(e);
			return n.getSiblings(e).every(function(t) {
				return r(e, t) || !n.isTag(t) || n.getName(t) !== i;
			});
		},
		"only-child": function(e, t) {
			var n = t.adapter, r = t.equals;
			return n.getSiblings(e).every(function(t) {
				return r(e, t) || !n.isTag(t);
			});
		}
	};
	function t(e, t, n, r) {
		if (n === null) {
			if (e.length > r) throw Error(`Pseudo-class :${t} requires an argument`);
		} else if (e.length === r) throw Error(`Pseudo-class :${t} doesn't have any arguments`);
	}
	e.verifyPseudoArgs = t;
})), fe = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.aliases = void 0, e.aliases = {
		"any-link": `:is(a, area, link)[href]`,
		link: `:any-link:not(:visited)`,
		disabled: `:is(
        :is(button, input, select, textarea, optgroup, option)[disabled],
        optgroup[disabled] > option,
        fieldset[disabled]:not(fieldset[disabled] legend:first-of-type *)
    )`,
		enabled: `:not(:disabled)`,
		checked: `:is(:is(input[type=radio], input[type=checkbox])[checked], option:selected)`,
		required: `:is(input, select, textarea)[required]`,
		optional: `:is(input, select, textarea):not([required])`,
		selected: `option:is([selected], select:not([multiple]):not(:has(> option[selected])) > :first-of-type)`,
		checkbox: `[type=checkbox]`,
		file: `[type=file]`,
		password: `[type=password]`,
		radio: `[type=radio]`,
		reset: `[type=reset]`,
		image: `[type=image]`,
		submit: `[type=submit]`,
		parent: `:not(:empty)`,
		header: `:is(h1, h2, h3, h4, h5, h6)`,
		button: `:is(button, input[type=button])`,
		input: `:is(input, textarea, select, button)`,
		text: `input:is(:not([type!='']), [type=text])`
	};
})), Q = e(((e) => {
	var t = e && e.__spreadArray || function(e, t, n) {
		if (n || arguments.length === 2) for (var r = 0, i = t.length, a; r < i; r++) (a || !(r in t)) && (a ||= Array.prototype.slice.call(t, 0, r), a[r] = t[r]);
		return e.concat(a || Array.prototype.slice.call(t));
	}, n = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.subselects = e.getNextSiblings = e.ensureIsTag = e.PLACEHOLDER_ELEMENT = void 0;
	var r = n(i()), a = Z();
	e.PLACEHOLDER_ELEMENT = {};
	function o(e, t) {
		return e === r.default.falseFunc ? r.default.falseFunc : function(n) {
			return t.isTag(n) && e(n);
		};
	}
	e.ensureIsTag = o;
	function s(e, t) {
		var n = t.getSiblings(e);
		if (n.length <= 1) return [];
		var r = n.indexOf(e);
		return r < 0 || r === n.length - 1 ? [] : n.slice(r + 1).filter(t.isTag);
	}
	e.getNextSiblings = s;
	function c(e) {
		return {
			xmlMode: !!e.xmlMode,
			lowerCaseAttributeNames: !!e.lowerCaseAttributeNames,
			lowerCaseTags: !!e.lowerCaseTags,
			quirksMode: !!e.quirksMode,
			cacheResults: !!e.cacheResults,
			pseudos: e.pseudos,
			adapter: e.adapter,
			equals: e.equals
		};
	}
	var l = function(e, t, n, i, a) {
		var o = a(t, c(n), i);
		return o === r.default.trueFunc ? e : o === r.default.falseFunc ? r.default.falseFunc : function(t) {
			return o(t) && e(t);
		};
	};
	e.subselects = {
		is: l,
		matches: l,
		where: l,
		not: function(e, t, n, i, a) {
			var o = a(t, c(n), i);
			return o === r.default.falseFunc ? e : o === r.default.trueFunc ? r.default.falseFunc : function(t) {
				return !o(t) && e(t);
			};
		},
		has: function(n, i, l, u, d) {
			var f = l.adapter, p = c(l);
			p.relativeSelector = !0;
			var m = i.some(function(e) {
				return e.some(a.isTraversal);
			}) ? [e.PLACEHOLDER_ELEMENT] : void 0, h = d(i, p, m);
			if (h === r.default.falseFunc) return r.default.falseFunc;
			var g = o(h, f);
			if (m && h !== r.default.trueFunc) {
				var _ = h.shouldTestNextSiblings, v = _ !== void 0 && _;
				return function(e) {
					if (!n(e)) return !1;
					m[0] = e;
					var r = f.getChildren(e), i = v ? t(t([], r, !0), s(e, f), !0) : r;
					return f.existsOne(g, i);
				};
			}
			return function(e) {
				return n(e) && f.existsOne(g, f.getChildren(e));
			};
		}
	};
})), $ = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.compilePseudoSelector = e.aliases = e.pseudos = e.filters = void 0;
	var t = (X(), r(Y)), n = ue();
	Object.defineProperty(e, "filters", {
		enumerable: !0,
		get: function() {
			return n.filters;
		}
	});
	var i = de();
	Object.defineProperty(e, "pseudos", {
		enumerable: !0,
		get: function() {
			return i.pseudos;
		}
	});
	var a = fe();
	Object.defineProperty(e, "aliases", {
		enumerable: !0,
		get: function() {
			return a.aliases;
		}
	});
	var o = Q();
	function s(e, r, s, c, l) {
		var u = r.name, d = r.data;
		if (Array.isArray(d)) {
			if (!(u in o.subselects)) throw Error(`Unknown pseudo-class :${u}(${d})`);
			return o.subselects[u](e, d, s, c, l);
		}
		var f = s.pseudos?.[u], p = typeof f == `string` ? f : a.aliases[u];
		if (typeof p == `string`) {
			if (d != null) throw Error(`Pseudo ${u} doesn't have any arguments`);
			var m = (0, t.parse)(p);
			return o.subselects.is(e, m, s, c, l);
		}
		if (typeof f == `function`) return (0, i.verifyPseudoArgs)(f, u, d, 1), function(t) {
			return f(t, d) && e(t);
		};
		if (u in n.filters) return n.filters[u](e, d, s, c);
		if (u in i.pseudos) {
			var h = i.pseudos[u];
			return (0, i.verifyPseudoArgs)(h, u, d, 2), function(t) {
				return h(t, s, d) && e(t);
			};
		}
		throw Error(`Unknown pseudo-class :${u}`);
	}
	e.compilePseudoSelector = s;
})), pe = e(((e) => {
	Object.defineProperty(e, "__esModule", { value: !0 }), e.compileGeneralSelector = void 0;
	var t = oe(), n = $(), i = (X(), r(Y));
	function a(e, t) {
		var n = t.getParent(e);
		return n && t.isTag(n) ? n : null;
	}
	function o(e, r, o, s, c) {
		var l = o.adapter, u = o.equals;
		switch (r.type) {
			case i.SelectorType.PseudoElement: throw Error(`Pseudo-elements are not supported by css-select`);
			case i.SelectorType.ColumnCombinator: throw Error(`Column combinators are not yet supported by css-select`);
			case i.SelectorType.Attribute:
				if (r.namespace != null) throw Error(`Namespaced attributes are not yet supported by css-select`);
				return (!o.xmlMode || o.lowerCaseAttributeNames) && (r.name = r.name.toLowerCase()), t.attributeRules[r.action](e, r, o);
			case i.SelectorType.Pseudo: return (0, n.compilePseudoSelector)(e, r, o, s, c);
			case i.SelectorType.Tag:
				if (r.namespace != null) throw Error(`Namespaced tag names are not yet supported by css-select`);
				var d = r.name;
				return (!o.xmlMode || o.lowerCaseTags) && (d = d.toLowerCase()), function(t) {
					return l.getName(t) === d && e(t);
				};
			case i.SelectorType.Descendant:
				if (o.cacheResults === !1 || typeof WeakSet > `u`) return function(t) {
					for (var n = t; n = a(n, l);) if (e(n)) return !0;
					return !1;
				};
				var f = /* @__PURE__ */ new WeakSet();
				return function(t) {
					for (var n = t; n = a(n, l);) if (!f.has(n)) {
						if (l.isTag(n) && e(n)) return !0;
						f.add(n);
					}
					return !1;
				};
			case `_flexibleDescendant`: return function(t) {
				var n = t;
				do
					if (e(n)) return !0;
				while (n = a(n, l));
				return !1;
			};
			case i.SelectorType.Parent: return function(t) {
				return l.getChildren(t).some(function(t) {
					return l.isTag(t) && e(t);
				});
			};
			case i.SelectorType.Child: return function(t) {
				var n = l.getParent(t);
				return n != null && l.isTag(n) && e(n);
			};
			case i.SelectorType.Sibling: return function(t) {
				for (var n = l.getSiblings(t), r = 0; r < n.length; r++) {
					var i = n[r];
					if (u(t, i)) break;
					if (l.isTag(i) && e(i)) return !0;
				}
				return !1;
			};
			case i.SelectorType.Adjacent: return l.prevElementSibling ? function(t) {
				var n = l.prevElementSibling(t);
				return n != null && e(n);
			} : function(t) {
				for (var n = l.getSiblings(t), r, i = 0; i < n.length; i++) {
					var a = n[i];
					if (u(t, a)) break;
					l.isTag(a) && (r = a);
				}
				return !!r && e(r);
			};
			case i.SelectorType.Universal:
				if (r.namespace != null && r.namespace !== `*`) throw Error(`Namespaced universal selectors are not yet supported by css-select`);
				return e;
		}
	}
	e.compileGeneralSelector = o;
})), me = e(((e) => {
	var t = e && e.__createBinding || (Object.create ? (function(e, t, n, r) {
		r === void 0 && (r = n);
		var i = Object.getOwnPropertyDescriptor(t, n);
		(!i || (`get` in i ? !t.__esModule : i.writable || i.configurable)) && (i = {
			enumerable: !0,
			get: function() {
				return t[n];
			}
		}), Object.defineProperty(e, r, i);
	}) : (function(e, t, n, r) {
		r === void 0 && (r = n), e[r] = t[n];
	})), n = e && e.__setModuleDefault || (Object.create ? (function(e, t) {
		Object.defineProperty(e, "default", {
			enumerable: !0,
			value: t
		});
	}) : function(e, t) {
		e.default = t;
	}), a = e && e.__importStar || function(e) {
		if (e && e.__esModule) return e;
		var r = {};
		if (e != null) for (var i in e) i !== "default" && Object.prototype.hasOwnProperty.call(e, i) && t(r, e, i);
		return n(r, e), r;
	}, o = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.compileToken = e.compileUnsafe = e.compile = void 0;
	var s = (X(), r(Y)), c = o(i()), l = a(Z()), u = pe(), d = Q();
	function f(e, t, n) {
		var r = p(e, t, n);
		return (0, d.ensureIsTag)(r, t.adapter);
	}
	e.compile = f;
	function p(e, t, n) {
		return y(typeof e == `string` ? (0, s.parse)(e) : e, t, n);
	}
	e.compileUnsafe = p;
	function m(e) {
		return e.type === s.SelectorType.Pseudo && (e.name === `scope` || Array.isArray(e.data) && e.data.some(function(e) {
			return e.some(m);
		}));
	}
	var h = { type: s.SelectorType.Descendant }, g = { type: `_flexibleDescendant` }, _ = {
		type: s.SelectorType.Pseudo,
		name: `scope`,
		data: null
	};
	function v(e, t, n) {
		for (var r = t.adapter, i = !!n?.every(function(e) {
			var t = r.isTag(e) && r.getParent(e);
			return e === d.PLACEHOLDER_ELEMENT || t && r.isTag(t);
		}), a = 0, o = e; a < o.length; a++) {
			var c = o[a];
			if (!(c.length > 0 && (0, l.isTraversal)(c[0]) && c[0].type !== s.SelectorType.Descendant)) if (i && !c.some(m)) c.unshift(h);
			else continue;
			c.unshift(_);
		}
	}
	function y(e, t, n) {
		e.forEach(l.default), n = t.context ?? n;
		var r = Array.isArray(n), i = n && (Array.isArray(n) ? n : [n]);
		if (t.relativeSelector !== !1) v(e, t, i);
		else if (e.some(function(e) {
			return e.length > 0 && (0, l.isTraversal)(e[0]);
		})) throw Error("Relative selectors are not allowed when the `relativeSelector` option is disabled");
		var a = !1, o = e.map(function(e) {
			if (e.length >= 2) {
				var n = e[0], o = e[1];
				n.type !== s.SelectorType.Pseudo || n.name !== `scope` || (r && o.type === s.SelectorType.Descendant ? e[1] = g : (o.type === s.SelectorType.Adjacent || o.type === s.SelectorType.Sibling) && (a = !0));
			}
			return b(e, t, i);
		}).reduce(x, c.default.falseFunc);
		return o.shouldTestNextSiblings = a, o;
	}
	e.compileToken = y;
	function b(e, t, n) {
		return e.reduce(function(e, r) {
			return e === c.default.falseFunc ? c.default.falseFunc : (0, u.compileGeneralSelector)(e, r, t, n, y);
		}, t.rootFunc ?? c.default.trueFunc);
	}
	function x(e, t) {
		return t === c.default.falseFunc || e === c.default.trueFunc ? e : e === c.default.falseFunc || t === c.default.trueFunc ? t : function(n) {
			return e(n) || t(n);
		};
	}
})), he = e(((e) => {
	var t = e && e.__createBinding || (Object.create ? (function(e, t, n, r) {
		r === void 0 && (r = n);
		var i = Object.getOwnPropertyDescriptor(t, n);
		(!i || (`get` in i ? !t.__esModule : i.writable || i.configurable)) && (i = {
			enumerable: !0,
			get: function() {
				return t[n];
			}
		}), Object.defineProperty(e, r, i);
	}) : (function(e, t, n, r) {
		r === void 0 && (r = n), e[r] = t[n];
	})), n = e && e.__setModuleDefault || (Object.create ? (function(e, t) {
		Object.defineProperty(e, "default", {
			enumerable: !0,
			value: t
		});
	}) : function(e, t) {
		e.default = t;
	}), r = e && e.__importStar || function(e) {
		if (e && e.__esModule) return e;
		var r = {};
		if (e != null) for (var i in e) i !== "default" && Object.prototype.hasOwnProperty.call(e, i) && t(r, e, i);
		return n(r, e), r;
	}, a = e && e.__importDefault || function(e) {
		return e && e.__esModule ? e : { default: e };
	};
	Object.defineProperty(e, "__esModule", { value: !0 }), e.aliases = e.pseudos = e.filters = e.is = e.selectOne = e.selectAll = e.prepareContext = e._compileToken = e._compileUnsafe = e.compile = void 0;
	var o = r(T()), s = a(i()), c = me(), l = Q(), u = function(e, t) {
		return e === t;
	}, d = {
		adapter: o,
		equals: u
	};
	function f(e) {
		var t = e ?? d;
		return t.adapter ??= o, t.equals ??= t.adapter?.equals ?? u, t;
	}
	function p(e) {
		return function(t, n, r) {
			return e(t, f(n), r);
		};
	}
	e.compile = p(c.compile), e._compileUnsafe = p(c.compileUnsafe), e._compileToken = p(c.compileToken);
	function m(e) {
		return function(t, n, r) {
			var i = f(r);
			typeof t != `function` && (t = (0, c.compileUnsafe)(t, i, n));
			var a = h(n, i.adapter, t.shouldTestNextSiblings);
			return e(t, a, i);
		};
	}
	function h(e, t, n) {
		return n === void 0 && (n = !1), n && (e = g(e, t)), Array.isArray(e) ? t.removeSubsets(e) : t.getChildren(e);
	}
	e.prepareContext = h;
	function g(e, t) {
		for (var n = Array.isArray(e) ? e.slice(0) : [e], r = n.length, i = 0; i < r; i++) {
			var a = (0, l.getNextSiblings)(n[i], t);
			n.push.apply(n, a);
		}
		return n;
	}
	e.selectAll = m(function(e, t, n) {
		return e === s.default.falseFunc || !t || t.length === 0 ? [] : n.adapter.findAll(e, t);
	}), e.selectOne = m(function(e, t, n) {
		return e === s.default.falseFunc || !t || t.length === 0 ? null : n.adapter.findOne(e, t);
	});
	function _(e, t, n) {
		var r = f(n);
		return (typeof t == `function` ? t : (0, c.compile)(t, r))(e);
	}
	e.is = _, e.default = e.selectAll;
	var v = $();
	Object.defineProperty(e, "filters", {
		enumerable: !0,
		get: function() {
			return v.filters;
		}
	}), Object.defineProperty(e, "pseudos", {
		enumerable: !0,
		get: function() {
			return v.pseudos;
		}
	}), Object.defineProperty(e, "aliases", {
		enumerable: !0,
		get: function() {
			return v.aliases;
		}
	});
}));
export { Y as es_exports, X as init_es, he as require_lib };
