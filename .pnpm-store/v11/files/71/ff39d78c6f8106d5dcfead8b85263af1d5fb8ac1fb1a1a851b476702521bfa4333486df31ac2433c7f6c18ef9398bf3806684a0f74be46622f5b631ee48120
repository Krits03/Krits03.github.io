interface DefinedRegion extends Thing {
    /**
     * The two-letter country code, in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1) format.
     */
    addressCountry: string;
    /**
     * If you include this property, the region must be a 2- or 3-digit ISO 3166-2 subdivision code, without country prefix. Currently, Google Search only supports the US, Australia, and Japan. Examples: "NY" (for US, state of New York), "NSW" (for Australia, state of New South Wales), or "03" (for Japan, Iwate prefecture).
     *
     * Do not provide both a region and postal code information.
     */
    addressRegion?: string;
    /**
     * The postal code. For example, 94043. Currently postal codes are supported for Australia, Canada, and the US.
     */
    postalCode?: string;
}

interface MonetaryAmountSimple extends Thing {
    /**
     * The currency in which the monetary amount is expressed.
     */
    currency: string;
    /**
     * The value of the quantitative value or property value node.
     */
    value: number | QuantitativeValue;
}
interface MonetaryAmount extends MonetaryAmountSimple {
}
interface QuantitativeSimple extends Thing {
    value?: number;
    minValue?: number;
    maxValue?: number;
    unitCode?: string;
    unitText?: 'HOUR' | 'DAY' | 'WEEK' | 'MONTH' | 'YEAR';
}
interface QuantitativeValue extends QuantitativeSimple {
}

interface ShippingDeliveryTime extends Thing {
    /**
     * The typical delay between the receipt of the order and the goods leaving the warehouse.
     */
    handlingTime?: QuantitativeValue;
    /**
     * The typical delay between when the order has been sent for delivery and when the goods reach the final customer.
     */
    transitTime?: QuantitativeValue;
}

interface OfferShippingDetails extends Thing {
    '@type'?: 'OfferShippingDetails';
    /**
     * The total delay between the receipt of the order and the goods reaching the final customer.
     */
    'deliveryTime': ShippingDeliveryTime;
    'shippingDestination': DefinedRegion;
    /**
     * Information about the cost of shipping to the specified destination. At least one of shippingRate.value or shippingRate.maxValue must be specified, along with shippingRate.currency.
     *
     * You can only specify one shippingRate per OfferShippingDetails property. To indicate multiple rates for your product, specify multiple OfferShippingDetail properties.
     */
    'shippingRate': MonetaryAmount;
}

type DayOfWeek = 'Friday' | 'Monday' | 'PublicHolidays' | 'Saturday' | 'Sunday' | 'Thursday' | 'Tuesday' | 'Wednesday';
type Time = `${number}${number}:${number}${number}`;
interface OpeningHoursSimple extends Thing {
    '@type'?: 'OpeningHoursSpecification';
    /**
     * The day of the week for which these opening hours are valid.
     */
    'dayOfWeek': Arrayable<DayOfWeek>;
    /**
     * The opening hour of the place or service on the given day(s) of the week.
     */
    'opens'?: Time;
    /**
     * The closing hour of the place or service on the given day(s) of the week.
     */
    'closes'?: Time;
    /**
     * The date when the item becomes valid.
     */
    'validFrom'?: ResolvableDate;
    /**
     * The date after when the item is not valid. For example, the end of an offer, salary period, or a period of opening hours.
     */
    'validThrough'?: ResolvableDate;
}
interface OpeningHoursSpecification extends OpeningHoursSimple {
}
declare const openingHoursResolver: SchemaOrgNodeDefinition<OpeningHoursSpecification>;

type ItemAvailability = 'BackOrder' | 'Discontinued' | 'InStock' | 'InStoreOnly' | 'LimitedAvailability' | 'OnlineOnly' | 'OutOfStock' | 'PreOrder' | 'PreSale' | 'SoldOut';
type OfferItemCondition = 'NewCondition' | 'RefurbishedCondition' | 'UsedCondition';
interface OfferSimple extends Thing {
    '@type'?: 'Offer';
    /**
     * Condition of the item offered for sale.
     */
    'itemCondition'?: OptionalSchemaOrgPrefix<OfferItemCondition>;
    /**
     * A schema.org URL representing a schema itemAvailability value (e.g., https://schema.org/OutOfStock).
     */
    'availability'?: OptionalSchemaOrgPrefix<ItemAvailability>;
    /**
     * The price, omitting any currency symbols, and using '.' to indicate a decimal place.
     */
    'price': number | string;
    /**
     * The currency used to describe the product price, in three-letter ISO 4217 format.
     */
    'priceCurrency'?: string;
    /**
     * @todo A PriceSpecification object, including a valueAddedTaxIncluded property (of either true or false).
     */
    'priceSpecification'?: unknown;
    /**
     * The date after which the price is no longer available.
     */
    'priceValidUntil'?: ResolvableDate;
    'url'?: string;
    /**
     * Nested information about the return policies associated with an Offer. If you decide to add hasMerchantReturnPolicy, add the required and recommended MerchantReturnPolicy properties.
     */
    'hasMerchantReturnPolicy'?: NodeRelation<OpeningHoursSpecification>;
    /**
     * Nested information about the shipping policies and options associated with an Offer. If you decide to add shippingDetails, add the required and recommended OfferShippingDetails properties.
     */
    'shippingDetails'?: OfferShippingDetails;
}
interface Offer extends OfferSimple {
}
declare const offerResolver: SchemaOrgNodeDefinition<Offer>;

interface AggregateOfferSimple extends Thing {
    /**
     * The lowest price of the group, omitting any currency symbols, and using '.' to indicate a decimal place.
     */
    lowPrice: number | string;
    /**
     *  The highest price of the group, omitting any currency symbols, and using '.' to indicate a decimal place.
     */
    highPrice: number | string;
    /**
     * The currency used to describe the product price, in a three-letter ISO 4217 format.
     */
    priceCurrency?: string;
    /**
     * The number of offers in the group
     */
    offerCount?: number | string;
    /**
     * An array of Offer pieces, referenced by ID.
     */
    offers?: NodeRelations<Offer>;
}
interface AggregateOffer extends AggregateOfferSimple {
}
declare const aggregateOfferResolver: SchemaOrgNodeDefinition<AggregateOffer>;

interface AggregateRatingSimple extends Thing {
    '@type'?: 'AggregateRating';
    /**
     * The total number of ratings for the item on your site. At least one of ratingCount or reviewCount is required.
     */
    'ratingCount'?: number | string;
    /**
     * Specifies the number of people who provided a review with or without an accompanying rating. At least one of ratingCount or reviewCount is required.
     */
    'reviewCount'?: number | string;
    /**
     * A numerical quality rating for the item, either a number, fraction, or percentage
     * (for example, "4", "60%", or "6 / 10").
     * Google understands the scale for fractions and percentages,
     * since the scale is implied in the fraction itself or the percentage.
     * The default scale for numbers is a 5-point scale, where 1 is the lowest value and 5 is the highest value.
     * If another scale is intended, use bestRating and worstRating.
     */
    'ratingValue': number | string;
    /**
     * The highest value allowed in this rating system. If bestRating is omitted, 5 is assumed.
     */
    'bestRating'?: number | string;
    /**
     * The lowest value allowed in this rating system. If worstRating is omitted, 1 is assumed.
     */
    'worstRating'?: number | string;
}
interface AggregateRating extends AggregateRatingSimple {
}
declare const aggregateRatingResolver: SchemaOrgNodeDefinition<AggregateRating>;

interface ImageSimple extends Thing {
    /**
     * The URL of the image file (e.g., /images/cat.jpg).
     */
    url: string;
    /**
     * The fully-qualified, absolute URL of the image file (e.g., https://www.example.com/images/cat.jpg).
     * Note: The contentUrl and url properties are intentionally duplicated.
     */
    contentUrl?: string;
    /**
     * A text string describing the image.
     * - Fall back to the image alt attribute if no specific caption field exists or is defined.
     */
    caption?: string;
    /**
     * The height of the image in pixels.
     * - Must be used with width.
     */
    height?: number;
    /**
     * The width of the image in pixels.
     * - Must be used with height.
     */
    width?: number;
    /**
     * The language code for the textual content; e.g., en-GB.
     * - Only needed when providing a caption.
     */
    inLanguage?: string;
    /**
     * The name of the image.
     */
    name?: string;
    /**
     * A description of the image.
     */
    description?: string;
    /**
     * The file format or media type of the image (e.g., image/jpeg).
     */
    encodingFormat?: string;
}
interface ImageObject extends ImageSimple {
}
/**
 * Describes an individual image (usually in the context of an embedded media object).
 */
declare const imageResolver: SchemaOrgNodeDefinition<ImageObject>;

interface VideoSimple extends Thing {
    /**
     * The title of the video.
     */
    name?: string;
    /**
     * A description of the video (falling back to the caption, then to 'No description').
     */
    description?: string;
    /**
     * A reference-by-ID to an imageObject.
     */
    thumbnail?: NodeRelation<ImageObject>;
    /**
     * A URL pointing to the video thumbnail image file. Follow the [thumbnail image guidelines](https://developers.google.com/search/docs/appearance/video#provide-a-high-quality-thumbnail).
     */
    thumbnailUrl?: Arrayable<string>;
    /**
     * The date the video was published, in ISO 8601 format (e.g., 2020-01-20).
     */
    uploadDate?: ResolvableDate;
    /**
     * Whether the video should be considered 'family friendly'
     */
    isFamilyFriendly?: boolean;
    /**
     * The URL of the image file (e.g., /images/cat.jpg).
     */
    url: string;
    /**
     * The fully-qualified, absolute URL of the image file (e.g., https://www.example.com/images/cat.jpg).
     * Note: The contentUrl and url properties are intentionally duplicated.
     */
    contentUrl?: string;
    /**
     * A text string describing the image.
     * - Fall back to the image alt attribute if no specific caption field exists or is defined.
     */
    caption?: string;
    /**
     * The height of the image in pixels.
     * - Must be used with width.
     */
    height?: number;
    /**
     * The width of the image in pixels.
     * - Must be used with height.
     */
    width?: number;
    /**
     * The language code for the textual content; e.g., en-GB.
     * - Only needed when providing a caption.
     */
    inLanguage?: string;
    /**
     * The duration of the video in ISO 8601 format.
     */
    duration?: string;
    /**
     * A URL pointing to a player for the video.
     */
    embedUrl?: string;
    /**
     * The encoding format of the video.
     */
    encodingFormat?: string;
    /**
     * A transcript of the video.
     */
    transcript?: string;
}
interface VideoObject extends VideoSimple {
}
/**
 * Describes an individual video (usually in the context of an embedded media object).
 */
declare const videoResolver: SchemaOrgNodeDefinition<VideoObject>;

type ValidArticleSubTypes = 'Article' | 'BlogPosting' | 'AdvertiserContentArticle' | 'NewsArticle' | 'Report' | 'SatiricalArticle' | 'ScholarlyArticle' | 'SocialMediaPosting' | 'TechArticle';
interface ArticleSimple extends Thing {
    ['@type']?: Arrayable<ValidArticleSubTypes>;
    /**
     * The headline of the article (falling back to the title of the WebPage).
     * Headlines should not exceed 110 characters.
     */
    headline?: string;
    /**
     * A summary of the article (falling back to the page's meta description content).
     */
    description?: string;
    /**
     * A reference-by-ID to the WebPage node.
     */
    isPartOf?: IdReference;
    /**
     * The time at which the article was originally published, in ISO 8601 format; e.g., 2015-10-31T16:10:29+00:00.
     */
    datePublished?: ResolvableDate;
    /**
     * The time at which the article was last modified, in ISO 8601 format; e.g., 2015-10-31T16:10:29+00:00.
     */
    dateModified?: ResolvableDate;
    /**
     * A reference-by-ID to the author of the article.
     */
    author?: NodeRelations<Identity>;
    /**
     * A reference-by-ID to the publisher of the article.
     */
    publisher?: NodeRelations<Identity>;
    /**
     * An array of all videos in the article content, referenced by ID.
     */
    video?: NodeRelations<VideoObject>;
    /**
     * An image object or referenced by ID.
     * - Must be at least 696 pixels wide.
     * - Must be of the following formats+file extensions: .jpg, .png, .gif ,or .webp.
     *
     * Must have markup of it somewhere on the page.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * An array of references by ID to comment pieces.
     */
    comment?: NodeRelations<Comment>;
    /**
     * A thumbnail image relevant to the Article.
     */
    thumbnailUrl?: string;
    /**
     * An integer value of the number of comments associated with the article.
     */
    commentCount?: number;
    /**
     * An integer value of the number of words in the article.
     */
    wordCount?: number;
    /**
     * An array of keywords which the article has (e.g., ["cats","dogs","cake"]).
     */
    keywords?: string[];
    /**
     * An array of category names which the article belongs to (e.g., ["cats","dogs","cake"]).
     */
    articleSection?: string[];
    /**
     * The language code for the article; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * A SpeakableSpecification object which identifies any content elements suitable for spoken results.
     */
    speakable?: unknown;
    /**
     * The year from which the article holds copyright status.
     */
    copyrightYear?: string;
    /**
     * A reference-by-ID to the Organization or Person who holds the copyright.
     */
    copyrightHolder?: NodeRelations<Identity>;
    /**
     * The body text of the article.
     */
    articleBody?: string;
    /**
     * The subject matter of the article.
     */
    about?: string;
}
interface Article extends ArticleSimple {
}
declare const PrimaryArticleId = "#article";
/**
 * Describes an Article on a WebPage.
 */
declare const articleResolver: SchemaOrgNodeDefinition<Article>;

/**
 * A list item, e.g. a step in a checklist or how-to description.
 */
interface ListItemSimple extends Thing {
    '@type'?: 'ListItem';
    /**
     *  The name of the page in question, as it appears in the breadcrumb navigation.
     */
    'name'?: string;
    /**
     * The unmodified canonical URL of the page in question.
     * - If a relative path is provided, it will be resolved to absolute.
     * - Item is not required for the last entry
     */
    'item'?: string | Thing;
    /**
     *  An integer (starting at 1), counting the 'depth' of the page from (including) the homepage.
     */
    'position'?: number;
}
interface ListItem extends ListItemSimple {
}
declare const listItemResolver: SchemaOrgNodeDefinition<ListItem>;

interface ItemListSimple extends Thing {
    /**
     * Resolved item list
     */
    itemListElement: NodeRelations<ListItem>;
    /**
     * Type of ordering (e.g. Ascending, Descending, Unordered).
     *
     * @default undefined
     */
    itemListOrder?: 'Ascending' | 'Descending' | 'Unordered';
    /**
     * The number of items in an ItemList.
     * Note that some descriptions might not fully describe all items in a list (e.g., multi-page pagination);
     * in such cases, the numberOfItems would be for the entire list.
     *
     * @default undefined
     */
    numberOfItems?: number;
}
interface ItemList extends ItemListSimple {
}
declare const itemListResolver: SchemaOrgNodeDefinition<ItemList>;

/**
 * A BreadcrumbList is an ItemList consisting of a chain of linked Web pages,
 * typically described using at least their URL and their name, and typically ending with the current page.
 */
interface BreadcrumbSimple extends ItemList {
    '@type'?: 'BreadcrumbList';
}
interface BreadcrumbList extends BreadcrumbSimple {
}
declare const PrimaryBreadcrumbId = "#breadcrumb";
/**
 * Describes the hierarchical position a WebPage within a WebSite.
 */
declare const breadcrumbResolver: SchemaOrgNodeDefinition<BreadcrumbList>;

interface PostalAddressSimple extends Thing {
    /**
     * The building number and street (e.g., 123 fake road ).
     */
    streetAddress: string;
    /**
     * The postal code.
     */
    postalCode: string;
    /**
     * The two-digit country-code representing the country (e.g., US ).
     */
    addressCountry: string;
    /**
     * The town, city or equivalent.
     */
    addressLocality?: string;
    /**
     * The region or district.
     */
    addressRegion?: string;
    /**
     * A PO box number.
     */
    postOfficeBoxNumber?: string;
}
interface PostalAddressStrict extends PostalAddressSimple {
}
interface PostalAddressName extends Partial<PostalAddressSimple> {
}
type PostalAddress = PostalAddressStrict | PostalAddressName;
declare const addressResolver: SchemaOrgNodeDefinition<PostalAddress>;

/**
 * An organization such as a school, NGO, corporation, club, etc.
 */
interface OrganizationSimple extends Thing {
    /**
     * A reference-by-ID to an image of the organization's logo.
     *
     * - The image must be 112x112px, at a minimum.
     * - Make sure the image looks how you intend it to look on a purely white background
     * (for example, if the logo is mostly white or gray,
     * it may not look how you want it to look when displayed on a white background).
     */
    logo?: NodeRelation<ImageObject | string>;
    /**
     * The site's home URL.
     */
    url?: string;
    /**
     * The name of the Organization.
     */
    name: string;
    /**
     * An array of URLs representing declared social/authoritative profiles of the organization
     * (e.g., a Wikipedia page, or Facebook profile).
     */
    sameAs?: Arrayable<string>;
    /**
     * An array of images which represent the organization (including the logo ), referenced by ID.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * A reference-by-ID to an PostalAddress piece.
     */
    address?: NodeRelations<PostalAddress>;
    /**
     * The telephone number of the organization.
     */
    telephone?: string;
    /**
     * The email address of the organization.
     */
    email?: string;
    /**
     * The date the organization was founded.
     */
    foundingDate?: string;
}
interface Organization extends OrganizationSimple {
}
/**
 * Describes an organization (a company, business or institution).
 * Most commonly used to identify the publisher of a WebSite.
 *
 * May be transformed into a more specific type
 * (such as Corporation or LocalBusiness) if the required conditions are met.
 */
declare const organizationResolver: SchemaOrgNodeDefinition<Organization>;

/**
 * A person (alive, dead, undead, or fictional).
 */
interface PersonSimple extends Thing {
    /**
     * The full name of the Person.
     */
    name: string;
    /**
     * The user bio, truncated to 250 characters.
     */
    description?: string;
    /**
     * An array of URLs representing declared social/authoritative profiles of the person
     * (e.g., a Wikipedia page, or Facebook profile).
     */
    sameAs?: Arrayable<string>;
    /**
     * An array of images which represent the person, referenced by ID.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * The URL of the users' profile page (if they're affiliated with the site in question),
     * or to their personal homepage/website.
     */
    url?: string;
}
interface Person extends PersonSimple {
}
/**
 * Describes an individual person. Most commonly used to identify the author of a piece of content (such as an Article or Comment).
 */
declare const personResolver: SchemaOrgNodeDefinition<Person>;

type SearchTarget = string | `${string}{search_term_string}${string | undefined}`;
interface SearchActionInput {
    /**
     * An object of type EntryPoint, with a relative URL which describes the URL pattern of the internal search function
     * (e.g., /search?query={search_term_string}).
     */
    target?: SearchTarget;
    /**
     * Alias: The search term string as described in the target (e.g., search_term_string).
     * @default search_term_string
     */
    queryInput?: string;
}
interface SearchAction {
    '@type'?: 'SearchAction';
    /**
     * An object of type EntryPoint, with a relative URL which describes the URL pattern of the internal search function
     * (e.g., /search?query={search_term_string}).
     */
    'target': SearchTarget | {
        '@type'?: 'EntryPoint';
        'urlTemplate'?: SearchTarget;
    };
    /**
     * The search term string as described in the target (e.g., search_term_string).
     */
    'query-input'?: {
        '@type'?: 'PropertyValueSpecification';
        'valueRequired'?: boolean;
        'valueName'?: 'search_term_string';
    };
}
declare const searchActionResolver: SchemaOrgNodeDefinition<SearchAction>;

/**
 * A WebSite is a set of related web pages and other items typically served from a single web domain and accessible via URLs.
 */
interface WebSiteSimple extends Thing {
    /**
     * The site's home URL (excluding a trailing slash).
     */
    url?: string;
    /**
     * The name of the website.
     */
    name: string;
    /**
     * A description of the website (e.g., the site's tagline).
     */
    description?: string;
    /**
     * The date the website was first published.
     */
    datePublished?: ResolvableDate;
    /**
     * The date the website was last modified.
     */
    dateModified?: ResolvableDate;
    /**
     * A reference-by-ID to the Organization which publishes the WebSite
     * (or an array of Organization and Person in the case that the website represents an individual).
     */
    publisher?: NodeRelations<Identity>;
    /**
     * A SearchAction object describing the site's internal search.
     */
    potentialAction?: Arrayable<(SearchAction | unknown)>;
    /**
     * The language code for the WebSite; e.g., en-GB.
     * If the website is available in multiple languages, then output an array of inLanguage values.
     */
    inLanguage?: Arrayable<string>;
}
interface WebSite extends WebSiteSimple {
}
declare const PrimaryWebSiteId = "#website";
declare const webSiteResolver: SchemaOrgNodeDefinition<WebSite>;

interface ReadActionInput {
    target?: string[];
}
interface ReadAction {
    '@type'?: 'ReadAction';
    /**
     * An array of string URLs which describes the URL pattern of the read action
     * (e.g., /search?query={search_term_string}).
     */
    'target': string[];
}
declare const readActionResolver: SchemaOrgNodeDefinition<ReadAction>;

type ValidSubTypes = 'WebPage' | 'AboutPage' | 'CheckoutPage' | 'CollectionPage' | 'ContactPage' | 'FAQPage' | 'ItemPage' | 'MedicalWebPage' | 'ProfilePage' | 'QAPage' | 'RealEstateListing' | 'SearchResultsPage';
/**
 * A web page.
 * Every web page is implicitly assumed to be declared to be of type WebPage,
 * so the various properties about that webpage, such as breadcrumb may be used.
 */
interface WebPageSimple extends Thing {
    ['@type']?: Arrayable<ValidSubTypes>;
    /**
     * The unmodified canonical URL of the page.
     */
    url?: string;
    /**
     * The title of the page.
     */
    name?: string;
    /**
     * The page's meta description content.
     */
    description?: string;
    /**
     * A reference-by-ID to the WebSite node.
     */
    isPartOf?: NodeRelation<WebSite>;
    /**
     * A reference-by-ID to the Organisation node.
     * Note: Only for the home page.
     */
    about?: NodeRelation<Organization>;
    /**
     * A reference-by-ID to the author of the web page.
     */
    author?: NodeRelation<Person | string>;
    /**
     * The language code for the page; e.g., en-GB.
     */
    inLanguage?: Arrayable<string>;
    /**
     * The time at which the page was originally published, in ISO 8601 format; e.g., 2015-10-31T16:10:29+00:00.
     */
    datePublished?: ResolvableDate;
    /**
     * The time at which the page was last modified, in ISO 8601 format; e.g., 2015-10-31T16:10:29+00:00.
     */
    dateModified?: ResolvableDate;
    /**
     * A reference-by-ID to a node representing the page's featured image.
     */
    primaryImageOfPage?: NodeRelation<ImageObject | string>;
    /**
     * A reference-by-ID to a node representing the page's breadrumb structure.
     */
    breadcrumb?: NodeRelation<BreadcrumbList>;
    /**
     * An array of all videos in the page content, referenced by ID.
     */
    video?: NodeRelations<VideoObject>;
    /**
     * A SpeakableSpecification object which identifies any content elements suitable for spoken results.
     */
    speakable?: unknown;
    /**
     * The time at which the page was last reviewed, in ISO 8601 format.
     */
    lastReviewed?: string;
    /**
     * An array of keywords describing the page.
     */
    keywords?: string[];
    /**
     * Potential actions for this web page.
     *
     * Note it's on by default for most page types.
     */
    potentialAction?: Arrayable<(ReadAction | unknown)>;
}
interface WebPage extends WebPageSimple {
}
declare const PrimaryWebPageId = "#webpage";
declare const webPageResolver: SchemaOrgNodeDefinition<WebPage>;

interface BookSimple extends Thing {
    /**
     * The title of the book.
     */
    name: string;
    /**
     * A description of the book. Display limit of 60 characters.
     */
    description?: string;
    /**
     *  A reference to an Identity piece, representing author associated with the Book.
     */
    author?: NodeRelations<Identity>;
    /**
     * The URL on your website where the book is introduced or described.
     */
    url?: string;
    /**
     * The URL of a reference page that identifies the work. For example, a Wikipedia, Wikidata, VIAF, or Library of Congress page for the book.
     */
    sameAs?: Arrayable<string>;
    /**
     * The number of pages in the book.
     */
    numberOfPages?: number;
    /**
     * The illustrator(s) of the book.
     */
    illustrator?: NodeRelations<Identity>;
    /**
     * The edition(s) of the work.
     */
    workExample: NodeRelations<BookEdition>;
}
interface Book extends BookSimple {
}
type BookFormat = OptionalSchemaOrgPrefix<'AudiobookFormat'> | OptionalSchemaOrgPrefix<'EBook'> | OptionalSchemaOrgPrefix<'Hardcover'> | OptionalSchemaOrgPrefix<'Paperback'>;
interface BookEditionSimple extends Thing {
    /**
     * The title of the edition. Only use this when the title of the edition is different from the title of the work.
     */
    name?: string;
    /**
     * The format of the edition.
     */
    bookFormat: BookFormat;
    /**
     * The main language of the content in the edition. Use one of the two-letter codes from the list of ISO 639-1 alpha-2 codes.
     */
    inLanguage?: string;
    /**
     * The ISBN-13 of the edition. If you have ISBN-10, convert it into ISBN-13.
     */
    isbn: string;
    /**
     * The action to be triggered for users to purchase or download the book.
     */
    potentialAction?: Arrayable<ReadAction | any>;
    /**
     * The author(s) of the edition.
     */
    author?: NodeRelations<Identity>;
    /**
     * The edition information of the book. For example, 2nd Edition.
     */
    bookEdition?: string;
    /**
     * The date of publication of the edition in YYYY-MM-DD or YYYY format. This can be either a specific date or only a specific year.
     */
    datePublished?: ResolvableDate;
    /**
     * The external or other ID that unambiguously identifies this edition. Multiple identifiers are allowed. For more details, refer to PropertyValue (identifier).
     */
    identifier?: unknown;
    /**
     * The URL of a reference web page that unambiguously indicates the edition. For example, a Wikipedia page for this specific edition. Don't reuse the sameAs of the Work.
     */
    sameAs?: Arrayable<string>;
    /**
     * The URL on your website where the edition is introduced or described. It can be the same as workExample.target.urlTemplate.
     */
    url?: string;
}
interface BookEdition extends BookEditionSimple {
}
declare const bookEditionResolver: SchemaOrgNodeDefinition<BookEdition>;
declare const PrimaryBookId = "#book";
declare const bookResolver: SchemaOrgNodeDefinition<Book>;

interface CommentSimple extends Thing {
    /**
     * The textual content of the comment, stripping HTML tags.
     */
    text: string;
    /**
     *  A reference by ID to the parent Article (or WebPage, when no Article is present).
     */
    about?: IdReference;
    /**
     * A reference by ID to the Person who wrote the comment.
     */
    author: NodeRelation<Person>;
    /**
     * The date and time the comment was created.
     */
    dateCreated?: ResolvableDate;
    /**
     * The date and time the comment was last modified.
     */
    dateModified?: ResolvableDate;
    /**
     * The number of upvotes the comment has received.
     */
    upvoteCount?: number;
    /**
     * The number of downvotes the comment has received.
     */
    downvoteCount?: number;
}
interface Comment$1 extends CommentSimple {
}
/**
 * Describes a comment. Usually in the context of an Article or a WebPage.
 */
declare const commentResolver: SchemaOrgNodeDefinition<Comment$1>;

/**
 * A course or class offered by an educational institution.
 */
interface CourseSimple extends Thing {
    /**
     * The title of the course.
     */
    name: string;
    /**
     * A description of the course. Display limit of 60 characters.
     */
    description?: string;
    /**
     * The course code or identifier.
     */
    courseCode?: string;
    /**
     * The educational level of the course.
     */
    educationalLevel?: string;
    /**
     * The duration of the course.
     */
    timeRequired?: string;
    /**
     * A reference to an Organization piece, representing the organization offering the course.
     */
    provider?: NodeRelation<Organization>;
}
interface Course extends CourseSimple {
}
declare const courseResolver: SchemaOrgNodeDefinition<Course>;

interface PlaceSimple extends Thing {
    '@type'?: 'Place';
    'name': string;
    'address': NodeRelation<PostalAddress | string>;
    'latitude'?: number | string;
    'longitude'?: number | string;
}
interface Place extends PlaceSimple {
}
/**
 * Describes a HowTo guide, which contains a series of steps.
 */
declare const placeResolver: SchemaOrgNodeDefinition<Place>;

interface VirtualLocationSimple extends Thing {
    '@type'?: 'VirtualLocation';
    'url': string;
}
interface VirtualLocation extends VirtualLocationSimple {
}
/**
 * Describes a HowTo guide, which contains a series of steps.
 */
declare const virtualLocationResolver: SchemaOrgNodeDefinition<VirtualLocation>;

type EventAttendanceModeTypes = 'OfflineEventAttendanceMode' | 'OnlineEventAttendanceMode' | 'MixedEventAttendanceMode';
type EventStatusTypes = 'EventCancelled' | 'EventMovedOnline' | 'EventPostponed' | 'EventRescheduled' | 'EventScheduled';
interface EventSimple extends Thing {
    /**
     * Description of the event.
     * Describe all details of the event to make it easier for users to understand and attend the event.
     */
    description?: string;
    /**
     * The end date and time of the item (in ISO 8601 date format).
     */
    endDate?: ResolvableDate;
    /**
     * The eventAttendanceMode of an event indicates whether it occurs online, offline, or a mix.
     */
    eventAttendanceMode?: OptionalSchemaOrgPrefix<EventAttendanceModeTypes>;
    /**
     * An eventStatus of an event represents its status; particularly useful when an event is cancelled or rescheduled.
     */
    eventStatus?: OptionalSchemaOrgPrefix<EventStatusTypes>;
    /**
     * Repeated ImageObject or URL
     *
     * URL of an image or logo for the event or tour.
     * Including an image helps users understand and engage with your event.
     * We recommend that images are 1920px wide (the minimum width is 720px).
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * The location of the event.
     * There are different requirements depending on if the event is happening online or at a physical location
     */
    location?: NodeRelations<Place | VirtualLocation | string>;
    /**
     * An offer to provide this item—for example, an offer to sell a product,
     * rent the DVD of a movie, perform a service, or give away tickets to an event.
     * Use businessFunction to indicate the kind of transaction offered, i.e. sell, lease, etc.
     * This property can also be used to describe a Demand.
     * While this property is listed as expected on a number of common types, it can be used in others.
     * In that case, using a second type, such as Product or a subtype of Product, can clarify the nature of the offer.
     */
    offers?: NodeRelations<Offer | string>;
    /**
     * An organizer of an Event.
     */
    organizer?: NodeRelation<Identity>;
    /**
     * A performer at the event—for example, a presenter, musician, musical group or actor.
     */
    performer?: NodeRelation<Person>;
    /**
     * Used in conjunction with eventStatus for rescheduled or cancelled events.
     * This property contains the previously scheduled start date.
     * For rescheduled events, the startDate property should be used for the newly scheduled start date.
     * In the (rare) case of an event that has been postponed and rescheduled multiple times, this field may be repeated.
     */
    previousStartDate?: ResolvableDate;
    /**
     * The start date and time of the item (in ISO 8601 date format).
     */
    startDate?: ResolvableDate;
    /**
     * The duration of the item (movie, audio recording, event, etc.) in ISO 8601 date format.
     */
    duration?: string;
    /**
     * Indicates whether an event is accessible for free.
     */
    isAccessibleForFree?: boolean;
    /**
     * The total number of individuals that may attend an event or venue.
     */
    maximumAttendeeCapacity?: number;
}
interface Event extends EventSimple {
}
declare const PrimaryEventId = "#event";
/**
 * Describes an Event.
 */
declare const eventResolver: SchemaOrgNodeDefinition<Event>;

type ValidLocalBusinessSubTypes = 'AnimalShelter' | 'ArchiveOrganization' | 'AutomotiveBusiness' | 'ChildCare' | 'Dentist' | 'DryCleaningOrLaundry' | 'EmergencyService' | 'EmploymentAgency' | 'EntertainmentBusiness' | 'FinancialService' | 'FoodEstablishment' | 'GovernmentOffice' | 'HealthAndBeautyBusiness' | 'HomeAndConstructionBusiness' | 'InternetCafe' | 'LegalService' | 'Library' | 'LodgingBusiness' | 'MedicalBusiness' | 'ProfessionalService' | 'RadioStation' | 'RealEstateAgent' | 'RecyclingCenter' | 'SelfStorage' | 'ShoppingCenter' | 'SportsActivityLocation' | 'Store' | 'TelevisionStation' | 'TouristInformationCenter' | 'TravelAgency';
interface LocalBusinessSimple extends Organization {
    '@type'?: ['Organization', 'LocalBusiness'] | ['Organization', 'LocalBusiness', ValidLocalBusinessSubTypes] | ValidLocalBusinessSubTypes;
    /**
     * The primary public telephone number of the business.
     */
    'telephone'?: string;
    /**
     * The primary public email address of the business.
     */
    'email'?: string;
    /**
     * The primary public fax number of the business.
     */
    'faxNumber'?: string;
    /**
     * The price range of the business, represented by a string of dollar symbols (e.g., $, $$, or $$$ ).
     */
    'priceRange'?: string;
    /**
     * An array of GeoShape, Place or string definitions.
     */
    'areaServed'?: unknown;
    /**
     * A GeoCoordinates object.
     */
    'geo'?: unknown;
    /**
     * The VAT ID of the business.
     */
    'vatID'?: string;
    /**
     * The tax ID of the business.
     */
    'taxID'?: string;
    /**
     * The currency accepted.
     */
    'currenciesAccepted'?: string;
    /**
     * The methods of payment accepted by the business.
     */
    'paymentAccepted'?: string;
    /**
     * The operating hours of the business.
     */
    'openingHoursSpecification'?: NodeRelations<OpeningHoursSpecification>;
}
interface LocalBusiness extends LocalBusinessSimple {
}
/**
 * Describes a business which allows public visitation.
 * Typically, used to represent the business 'behind' the website, or on a page about a specific business.
 */
declare const localBusinessResolver: SchemaOrgNodeDefinition<LocalBusiness>;

interface RatingSimple extends Thing {
    '@type'?: 'Rating';
    /**
     * A numerical quality rating for the item, either a number, fraction, or percentage
     * (for example, "4", "60%", or "6 / 10").
     * Google understands the scale for fractions and percentages,
     * since the scale is implied in the fraction itself or the percentage.
     * The default scale for numbers is a 5-point scale, where 1 is the lowest value and 5 is the highest value.
     * If another scale is intended, use bestRating and worstRating.
     */
    'ratingValue': number | string;
    /**
     * The highest value allowed in this rating system. If bestRating is omitted, 5 is assumed.
     */
    'bestRating'?: number;
    /**
     * The lowest value allowed in this rating system. If worstRating is omitted, 1 is assumed.
     */
    'worstRating'?: number;
}
interface Rating extends RatingSimple {
}
declare const ratingResolver: SchemaOrgNodeDefinition<Rating>;

type ValidFoodEstablishmentSubTypes = 'Bakery' | 'BarOrPub' | 'Brewery' | 'Dentist' | 'CafeOrCoffeeShop' | 'Distillery' | 'FastFoodRestaurant' | 'IceCreamShop' | 'Restaurant' | 'Winery';
interface FoodEstablishmentSimple extends Omit<LocalBusiness, '@type'> {
    '@type'?: ['Organization', 'LocalBusiness', 'FoodEstablishment'] | ['Organization', 'LocalBusiness', 'FoodEstablishment', ValidFoodEstablishmentSubTypes] | ValidFoodEstablishmentSubTypes;
    /**
     * Indicates whether a FoodEstablishment accepts reservations.
     */
    'acceptsReservations'?: string | boolean;
    /**
     * URL of the menu.
     */
    'hasMenu'?: string;
    /**
     * Methods of payment accepted.
     */
    'paymentAccepted'?: string;
    /**
     * The cuisine of the restaurant.
     */
    'servesCuisine'?: string;
    /**
     * An official rating for a lodging business or food establishment
     */
    'starRating'?: NodeRelations<Rating>;
}
interface FoodEstablishment extends FoodEstablishmentSimple {
}
/**
 * Describes a business which allows public visitation.
 * Typically, used to represent the business 'behind' the website, or on a page about a specific business.
 */
declare const foodEstablishmentResolver: SchemaOrgNodeDefinition<FoodEstablishment>;

interface HowToDirection extends Thing {
    /**
     * The text of the direction or tip.
     */
    text: string;
}
/**
 * Describes the text of a direction or tip for a step in a HowTo guide.
 */
declare const howToStepDirectionResolver: SchemaOrgNodeDefinition<HowToDirection>;

interface HowToStepSimple extends Thing {
    /**
     * A link to a fragment identifier (an 'ID anchor') of the individual step
     * (e.g., https://www.example.com/example-page/#recipe-step-5).
     */
    url?: string;
    /**
     * The instruction string
     * ("e.g., "Bake at 200*C for 40 minutes, or until golden-brown, stirring periodically throughout").
     */
    text: string;
    /**
     * The word or short phrase summarizing the step (for example, "Attach wires to post" or "Dig").
     * Don't use non-descriptive text (for example, "Step 1: [text]") or other form of step number (for example, "1. [text]").
     */
    name?: string;
    /**
     * An image representing the step, referenced by ID.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * A video for this step or a clip of the video.
     */
    video?: NodeRelations<VideoObject | string>;
    /**
     * A list of detailed substeps, including directions or tips.
     */
    itemListElement?: NodeRelations<HowToDirection | string>[];
}
interface HowToStep extends HowToStepSimple {
}
/**
 * Describes a HowTo guide, which contains a series of steps.
 */
declare const howToStepResolver: SchemaOrgNodeDefinition<HowToStep>;

/**
 * Instructions that explain how to achieve a result by performing a sequence of steps.
 */
interface HowToSimple extends Thing {
    /**
     * A string describing the guide.
     */
    name: string;
    /**
     * An array of howToStep objects
     */
    step: NodeRelations<HowToStep | string>[];
    /**
     * The total time required to perform all instructions or directions (including time to prepare the supplies),
     * in ISO 8601 duration format.
     */
    totalTime?: string;
    /**
     * Introduction or description content relating to the HowTo guide.
     */
    description?: string;
    /**
     * The language code for the guide; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * The estimated cost of the supplies consumed when performing instructions.
     */
    estimatedCost?: string | unknown;
    /**
     * Image of the completed how-to.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * A supply consumed when performing instructions or a direction.
     */
    supply?: string | unknown;
    /**
     * An object used (but not consumed) when performing instructions or a direction.
     */
    tool?: string | unknown;
    /**
     * A video of the how-to. Follow the list of required and recommended Video properties.
     * Mark steps of the video with hasPart.
     */
    video?: NodeRelations<VideoObject | string>;
    /**
     * The time required to prepare for the how-to, in ISO 8601 duration format.
     */
    prepTime?: string;
    /**
     * The time it takes to perform the how-to, in ISO 8601 duration format.
     */
    performTime?: string;
    /**
     * The quantity that results from performing the how-to.
     */
    yield?: string;
}
interface HowTo extends HowToSimple {
}
declare const HowToId = "#howto";
/**
 * Describes a HowTo guide, which contains a series of steps.
 */
declare const howToResolver: SchemaOrgNodeDefinition<HowTo>;

/**
 * A listing that describes a job opening in a certain organization.
 */
interface JobPostingSimple extends Thing {
    /**
     * The original date that employer posted the job in ISO 8601 format.
     * For example, "2017-01-24" or "2017-01-24T19:33:17+00:00".
     */
    datePosted: ResolvableDate;
    /**
     * The full description of the job in HTML format.
     *
     * The description must be a complete representation of the job, including job responsibilities, qualifications,
     * skills, working hours, education requirements, and experience requirements. The description can't be the same as
     * the title
     */
    description: string;
    /**
     * The organization offering the job position. This must be the name of the company (for example, "Starbucks, Inc"),
     * and not the specific location that is hiring (for example, "Starbucks on Main Street").
     */
    hiringOrganization: NodeRelation<Organization>;
    /**
     * The physical location(s) of the business where the employee will report to work (such as an office or worksite),
     * not the location where the job was posted. Include as many properties as possible. The more properties you provide,
     * the higher quality the job posting is to our users. Note that you must include the addressCountry property.
     */
    jobLocation: NodeRelation<Place>;
    /**
     * The title of the job (not the title of the posting). For example, "Software Engineer" or "Barista"
     */
    title: string;
    /**
     * The actual base salary for the job, as provided by the employer (not an estimate).
     */
    baseSalary?: MonetaryAmount;
    /**
     * Type of employment
     */
    employmentType?: EmploymentType | EmploymentType[];
    /**
     * The date when the job posting will expire in ISO 8601 format. For example, "2017-02-24"
     * or "2017-02-24T19:33:17+00:00".
     */
    validThrough?: ResolvableDate;
    /**
     * A description of the job location (e.g. TELECOMMUTE for telecommute jobs).
     */
    jobLocationType?: 'TELECOMMUTE';
    /**
     * Indicates whether the URL that's associated with this job posting enables direct application for the job.
     */
    directApply?: boolean;
    /**
     * Description of benefits associated with the job.
     */
    jobBenefits?: string;
    /**
     * Educational credentials or qualifications required for the job.
     */
    educationRequirements?: string;
    /**
     * Description of the level of experience required for the job.
     */
    experienceRequirements?: string;
    /**
     * Skills, abilities, or knowledge needed for the job.
     */
    qualifications?: string;
}
interface JobPosting extends JobPostingSimple {
}
declare const jobPostingResolver: SchemaOrgNodeDefinition<JobPosting>;
type EmploymentType = 'FULL_TIME' | 'PART_TIME' | 'CONTRACTOR' | 'TEMPORARY' | 'INTERN' | 'VOLUNTEER' | 'PER_DIEM' | 'OTHER';

interface ReviewSimple extends Thing {
    /**
     * A title for the review.
     */
    name?: string;
    /**
     * The author of the review.
     */
    author: NodeRelation<Person | string>;
    /**
     * An answer object, with a text property which contains the answer to the question.
     */
    reviewRating: NodeRelation<Rating | number>;
    /**
     * The language code for the question; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * The date that the review was published, in ISO 8601 date format.
     */
    datePublished?: ResolvableDate;
    /**
     * The text content of the review.
     */
    reviewBody?: string;
}
interface Review extends ReviewSimple {
}
declare const reviewResolver: SchemaOrgNodeDefinition<Review>;

interface MovieSimple extends Thing {
    /**
     * An image that represents the movie.
     */
    image: NodeRelations<string | ImageObject>;
    /**
     * The name of the movie.
     */
    name: string;
    /**
     * Annotation for the average review score assigned to the movie.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * The date the movie was released.
     */
    dateCreated?: ResolvableDate;
    /**
     * The director of the movie.
     */
    director?: NodeRelations<Person | string>;
    /**
     * The actor of the movie.
     */
    actor?: NodeRelations<Person | string>;
    /**
     * A nested Review of the movie.
     */
    review?: NodeRelations<Review>;
    /**
     * The trailer of a movie or TV/radio series, season, episode, etc.
     */
    trailer?: NodeRelations<string | VideoObject>;
    /**
     * The duration of the movie.
     */
    duration?: string;
    /**
     * The genre of the movie.
     */
    genre?: string;
    /**
     * The content rating of the movie.
     */
    contentRating?: string;
    /**
     * The production company of the movie.
     */
    productionCompany?: NodeRelation<Organization>;
}
interface Movie extends MovieSimple {
}
declare const movieResolver: SchemaOrgNodeDefinition<Movie>;

/**
 * Any offered product or service.
 * For example: a pair of shoes; a concert ticket; the rental of a car;
 * a haircut; or an episode of a TV show streamed online.
 */
interface ProductSimple extends Thing {
    /**
     * The name of the product.
     */
    name: string;
    /**
     * A reference-by-ID to one or more imageObject's which represent the product.
     * - Must be at least 696 pixels wide.
     * - Must be of the following formats+file extensions: .jpg, .png, .gif ,or .webp.
     */
    image: NodeRelations<ImageObject | string>;
    /**
     *  An array of references-by-ID to one or more Offer or aggregateOffer pieces.
     */
    offers?: NodeRelations<Offer | number>;
    /**
     *  A reference to an Organization piece, representing brand associated with the Product.
     */
    brand?: NodeRelation<Organization>;
    /**
     * A reference to an Organization piece which represents the seller/merchant.
     */
    seller?: NodeRelation<Organization>;
    /**
     * A text description of the product.
     */
    description?: string;
    /**
     * An array of references-by-id to one or more Review pieces.
     */
    review?: NodeRelations<Review>;
    /**
     * A merchant-specific identifier for the Product.
     */
    sku?: string;
    /**
     * The Global Trade Item Number (GTIN) of the product.
     */
    gtin?: string;
    /**
     * The Manufacturer Part Number (MPN) of the product.
     */
    mpn?: string;
    /**
     * The condition of the product (e.g., New, Used, Refurbished).
     */
    itemCondition?: string;
    /**
     * An AggregateRating object.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * An AggregateOffer object.
     */
    aggregateOffer?: NodeRelation<AggregateOffer>;
    /**
     * A reference to an Organization piece, representing the brand which produces the Product.
     */
    manufacturer?: NodeRelation<Organization>;
}
interface Product extends ProductSimple {
}
declare const ProductId = "#product";
declare const productResolver: SchemaOrgNodeDefinition<Product>;

/**
 * An answer offered to a question; perhaps correct, perhaps opinionated or wrong.
 */
interface AnswerSimple extends Thing {
    text: string;
}
interface Answer extends AnswerSimple {
}

/**
 * A specific question - e.g. from a user seeking answers online, or collected in a Frequently Asked Questions (FAQ) document.
 */
interface QuestionSimple extends Thing {
    /**
     * The text content of the question.
     */
    name: string;
    /**
     * An answer object, with a text property which contains the answer to the question.
     */
    acceptedAnswer: NodeRelation<Answer | string>;
    /**
     * The language code for the question; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * The number of answers provided for this question.
     */
    answerCount?: number;
    /**
     * The date and time the question was created.
     */
    dateCreated?: ResolvableDate;
    /**
     * Alias for `name`
     */
    question?: string;
    /**
     * Alias for `acceptedAnswer`
     */
    answer?: string;
}
interface Question extends QuestionSimple {
}
/**
 * Describes a Question. Most commonly used in FAQPage or QAPage content.
 */
declare const questionResolver: SchemaOrgNodeDefinition<Question>;

interface RecipeSimple extends Thing {
    /**
     * A string describing the recipe.
     */
    name?: string;
    /**
     * An image representing the completed recipe, referenced by ID.
     */
    image?: NodeRelation<ImageObject | string>;
    /**
     * An array of strings representing each ingredient and quantity (e.g., "3 apples").
     */
    recipeIngredient: string[];
    /**
     * An array of HowToStep objects.
     */
    recipeInstructions: NodeRelations<HowToStep | string>;
    /**
     * A string describing the recipe.
     */
    description?: string;
    /**
     * The cooking time in ISO 8601 format.
     */
    cookTime?: string;
    /**
     * The time required to prepare the recipe.
     */
    prepTime?: string;
    /**
     * The total time required to prepare and cook the recipe in ISO 8601 format.
     */
    totalTime?: string;
    /**
     * The cooking method used to prepare the recipe.
     */
    cookingMethod?: string;
    /**
     * A NutritionInformation node, with a calories property which defines a calorie count as a string (e.g., "270 calories").
     */
    nutrition?: NutritionInformation;
    /**
     * The number of servings the recipe creates (not the number of individual items, if these are different), as a string
     * (e.g., "6", rather than 6).
     */
    recipeYield?: string;
    /**
     * An array of strings representing the tools required in the recipe.
     */
    tools?: string[];
    /**
     * An array of keywords describing the recipe.
     */
    keywords?: string[];
    /**
     * A string describing the cuisine type (e.g., "American" or "Spanish").
     */
    recipeCuisine?: string;
    /**
     * The category of the recipe.
     */
    recipeCategory?: 'Appetizer' | 'Breakfast' | 'Brunch' | 'Dessert' | 'Dinner' | 'Drink' | 'Lunch' | 'Main course' | 'Sauce' | 'Side dish' | 'Snack' | 'Starter' | (string & Record<never, never>);
    /**
     * A RestrictedDiet node, with a value (or array of values
     */
    suitableForDiet?: Partial<'DiabeticDiet' | 'GlutenFreeDiet' | 'HalalDiet' | 'HinduDiet' | 'KosherDiet' | 'LowCalorieDiet' | 'LowFatDiet' | 'LowLactoseDiet' | 'LowSaltDiet' | 'VeganDiet' | 'VegetarianDiet'>[];
    /**
     *  A reference to a video representing the recipe instructions, by ID.
     */
    video?: NodeRelations<VideoObject | IdReference>;
    /**
     * The language code for the guide; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * A reference-by-ID to the author of the article.
     */
    author?: NodeRelation<Person>;
    /**
     * The date when the recipe was added, in ISO 8601 format.
     */
    datePublished?: ResolvableDate;
}
interface Recipe extends RecipeSimple {
}
interface NutritionInformation extends Thing {
    '@type': 'NutritionInformation';
    /**
     * A calorie count as a string (e.g., "270 calories").
     */
    'calories': string;
}
declare const RecipeId = "#recipe";
declare const recipeResolver: SchemaOrgNodeDefinition<Recipe>;

type ApplicationCategory = 'GameApplication' | 'SocialNetworkingApplication' | 'TravelApplication' | 'ShoppingApplication' | 'SportsApplication' | 'LifestyleApplication' | 'BusinessApplication' | 'DesignApplication' | 'DeveloperApplication' | 'DriverApplication' | 'EducationalApplication' | 'HealthApplication' | 'FinanceApplication' | 'SecurityApplication' | 'BrowserApplication' | 'CommunicationApplication' | 'DesktopEnhancementApplication' | 'EntertainmentApplication' | 'MultimediaApplication' | 'HomeApplication' | 'UtilitiesApplication' | 'ReferenceApplication';
interface SoftwareAppSimple extends Thing {
    '@type'?: Arrayable<'SoftwareApplication' | 'MobileApplication' | 'VideoGame' | 'WebApplication'>;
    /**
     * The name of the app.
     */
    'name'?: string;
    /**
     * An offer to sell the app.
     * For developers, offers can indicate the marketplaces that carry the application.
     * For marketplaces, use offers to indicate the price of the app for a specific app instance.
     */
    'offers': NodeRelations<Offer>;
    /**
     * The average review score of the app.
     */
    'aggregateRating'?: NodeRelation<AggregateRating>;
    /**
     * A single review of the app.
     */
    'review'?: NodeRelation<Review>;
    /**
     * The type of app (for example, BusinessApplication or GameApplication). The value must be a supported app type.
     */
    'applicationCategory'?: ApplicationCategory;
    /**
     * The operating system(s) required to use the app (for example, Windows 7, OSX 10.6, Android 1.6)
     */
    'operatingSystem'?: string;
    /**
     * A description of the app.
     */
    'description'?: string;
    /**
     * URL to download the app.
     */
    'downloadUrl'?: string;
    /**
     * The version of the app.
     */
    'softwareVersion'?: string;
    /**
     * A list of features offered by the app.
     */
    'featureList'?: string[];
}
interface SoftwareApp extends SoftwareAppSimple {
}
declare const softwareAppResolver: SchemaOrgNodeDefinition<SoftwareApp>;

type Arrayable<T> = T | Array<T>;
type NodeRelation<T> = T | IdReference;
type NodeRelations<T> = Arrayable<NodeRelation<T>>;
type Identity = Person | Organization;
type ResolvableDate = string | Date;
type OptionalSchemaOrgPrefix<T extends string> = T | `https://schema.org/${T}`;
interface ResolvedMeta {
    host: string;
    url: string;
    currency?: string;
    inLanguage?: string;
    image?: string;
    title?: string;
    description?: string;
    datePublished?: string;
    dateModified?: string;
    trailingSlash?: boolean;
}
interface MetaInput {
    /**
     * Whether to inject the scripts at the end of the body or in the head.
     */
    tagPosition?: 'body' | 'head';
    trailingSlash?: boolean;
    host: string;
    url?: string;
    path?: string;
    currency?: string;
    image?: string;
    inLanguage?: string;
    title?: string;
    description?: string;
    datePublished?: string;
    dateModified?: string;
    /**
     * @deprecated use tagPosition
     */
    position?: 'body' | 'head';
    /**
     * @deprecated use `language`
     */
    defaultLanguage?: string;
    /**
     * @deprecated use `currency`
     */
    defaultCurrency?: string;
    /**
     * @deprecated use `host`
     */
    canonicalHost?: string;
    /**
     * @deprecated use `url` or `path`
     */
    canonicalUrl?: string;
}
interface UserConfig extends MetaInput {
}
interface SchemaOrgNodeDefinition<ResolvedInput> {
    alias?: string;
    cast?: (node: any, ctx: SchemaOrgGraph) => ResolvedInput;
    idPrefix?: 'host' | 'url' | ['host' | 'url', string];
    inheritMeta?: (keyof ResolvedMeta | {
        key: keyof ResolvedInput;
        meta: keyof ResolvedMeta;
    })[];
    defaults?: Partial<ResolvedInput> | ((ctx: SchemaOrgGraph) => Partial<any>);
    required?: (keyof ResolvedInput)[];
    resolve?: (node: ResolvedInput, ctx: SchemaOrgGraph) => ResolvedInput;
    resolveRootNode?: (node: ResolvedInput, ctx: SchemaOrgGraph) => void;
}
interface Thing {
    '@type'?: Arrayable<string>;
    '@id'?: Id;
    /**
     * A reference-by-ID to the WebPage node.
     */
    'mainEntityOfPage'?: Arrayable<IdReference>;
    /**
     * A reference-by-ID to the WebPage node.
     */
    'mainEntity'?: Arrayable<IdReference>;
    /**
     * An image object or referenced by ID.
     * - Must be at least 696 pixels wide.
     * - Must be of the following formats+file extensions: .jpg, .png, .gif ,or .webp.
     */
    'image'?: NodeRelations<ImageObject | string>;
    /**
     * The work that this work has been translated from. E.g. 物种起源 is a translationOf “On the Origin of Species”.
     */
    'translationOfWork'?: NodeRelations<Thing>;
    /**
     * A work that is a translation of the content of this work. E.g. 西遊記 has an English workTranslation “Journey to the West”, a German workTranslation “Monkeys Pilgerfahrt” and a Vietnamese translation Tây du ký bình khảo.
     */
    'workTranslation'?: NodeRelations<Thing>;
    /**
     * Allow any arbitrary keys
     */
    [key: string]: any;
}
interface SchemaOrgNode extends Thing {
    _resolver?: SchemaOrgNodeDefinition<any>;
    _dedupeStrategy?: 'replace' | 'merge';
}
type WithResolver<T> = T & {
    _resolver?: SchemaOrgNodeDefinition<T>;
};
interface IdReference {
    /** IRI identifying the canonical address of this object. */
    '@id': string;
}
type Id = string | `#${string}` | `https://${string}#${string}`;

interface SchemaOrgGraph {
    nodes: SchemaOrgNode[];
    nodeIndex: Map<Id, SchemaOrgNode>;
    nodeIdCounters: Record<string, number>;
    meta: ResolvedMeta;
    push: <T extends Arrayable<Thing>>(node: T) => void;
    resolveGraph: (meta: MetaInput) => SchemaOrgNode[];
    find: <T extends Thing>(id: Id | string) => T | null;
}
declare function createSchemaOrgGraph(): SchemaOrgGraph;

export { virtualLocationResolver as $, commentResolver as E, courseResolver as H, PrimaryEventId as L, PrimaryArticleId as P, eventResolver as Q, placeResolver as Y, foodEstablishmentResolver as a2, HowToId as a5, howToResolver as a6, howToStepResolver as a9, organizationResolver as aC, personResolver as aF, addressResolver as aK, ProductId as aN, productResolver as aO, questionResolver as aR, ratingResolver as aU, RecipeId as aY, recipeResolver as aZ, howToStepDirectionResolver as ab, imageResolver as ae, itemListResolver as ah, jobPostingResolver as ak, listItemResolver as an, localBusinessResolver as aq, movieResolver as at, offerResolver as aw, openingHoursResolver as az, reviewResolver as b0, softwareAppResolver as b3, videoResolver as b6, PrimaryWebPageId as b9, webPageResolver as ba, readActionResolver as bd, PrimaryWebSiteId as bg, webSiteResolver as bh, searchActionResolver as bk, createSchemaOrgGraph as c, aggregateOfferResolver as j, aggregateRatingResolver as m, articleResolver as p, bookEditionResolver as t, PrimaryBookId as u, bookResolver as v, PrimaryBreadcrumbId as y, breadcrumbResolver as z };
export type { Arrayable as A, BookSimple as B, CommentSimple as C, Comment$1 as D, CourseSimple as F, Course as G, Id as I, EventSimple as J, Event as K, MetaInput as M, NodeRelation as N, OptionalSchemaOrgPrefix as O, ResolvedMeta as R, SchemaOrgNodeDefinition as S, Thing as T, UserConfig as U, PlaceSimple as V, WithResolver as W, Place as X, VirtualLocationSimple as Z, VirtualLocation as _, SchemaOrgGraph as a, Review as a$, FoodEstablishmentSimple as a0, FoodEstablishment as a1, HowToSimple as a3, HowTo as a4, HowToStepSimple as a7, HowToStep as a8, OrganizationSimple as aA, Organization as aB, PersonSimple as aD, Person as aE, PostalAddressSimple as aG, PostalAddressStrict as aH, PostalAddressName as aI, PostalAddress as aJ, ProductSimple as aL, Product as aM, QuestionSimple as aP, Question as aQ, RatingSimple as aS, Rating as aT, RecipeSimple as aV, Recipe as aW, NutritionInformation as aX, ReviewSimple as a_, HowToDirection as aa, ImageSimple as ac, ImageObject as ad, ItemListSimple as af, ItemList as ag, JobPostingSimple as ai, JobPosting as aj, ListItemSimple as al, ListItem as am, LocalBusinessSimple as ao, LocalBusiness as ap, MovieSimple as ar, Movie as as, OfferSimple as au, Offer as av, OpeningHoursSimple as ax, OpeningHoursSpecification as ay, Identity as b, SoftwareAppSimple as b1, SoftwareApp as b2, VideoSimple as b4, VideoObject as b5, WebPageSimple as b7, WebPage as b8, ReadActionInput as bb, ReadAction as bc, WebSiteSimple as be, WebSite as bf, SearchActionInput as bi, SearchAction as bj, IdReference as d, NodeRelations as e, ResolvableDate as f, SchemaOrgNode as g, AggregateOfferSimple as h, AggregateOffer as i, AggregateRatingSimple as k, AggregateRating as l, ArticleSimple as n, Article as o, Book as q, BookEditionSimple as r, BookEdition as s, BreadcrumbSimple as w, BreadcrumbList as x };
