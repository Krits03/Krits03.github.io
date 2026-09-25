import { T as Thing, A as Arrayable, e as NodeRelations, b as Identity, N as NodeRelation, f as ResolvableDate, S as SchemaOrgNodeDefinition, aE as Person, ad as ImageObject, l as AggregateRating, a$ as Review, aB as Organization, av as Offer, b5 as VideoObject, aJ as PostalAddress, aH as PostalAddressStrict, aI as PostalAddressName, i as AggregateOffer, o as Article, q as Book, s as BookEdition, x as BreadcrumbList, D as Comment, G as Course, K as Event, a1 as FoodEstablishment, a4 as HowTo, a8 as HowToStep, ag as ItemList, aj as JobPosting, am as ListItem, ap as LocalBusiness, as as Movie, ay as OpeningHoursSpecification, X as Place, aM as Product, aQ as Question, bc as ReadAction, aW as Recipe, bj as SearchAction, b2 as SoftwareApp, _ as VirtualLocation, b8 as WebPage, bf as WebSite } from './schema-org.CFcsqFfN.js';
import { Unhead, HeadEntryOptions, ActiveHeadEntry } from 'unhead/types';

/**
 * Represents a data download distribution.
 */
interface DataDownload extends Thing {
    '@type'?: 'DataDownload';
    /**
     * The direct download URL for the dataset file.
     */
    'contentUrl'?: string;
    /**
     * The file format of the distribution (e.g., "CSV", "JSON", "XML", "application/json").
     */
    'encodingFormat'?: string;
    /**
     * The size of the file in bytes or human-readable format (e.g., "1.5 MB").
     */
    'contentSize'?: string;
}
/**
 * Represents a data catalog that contains this dataset.
 */
interface DataCatalog extends Thing {
    '@type'?: 'DataCatalog';
    /**
     * The name of the data catalog.
     */
    'name'?: string;
    /**
     * The URL of the data catalog.
     */
    'url'?: string;
}
interface DatasetSimple extends Thing {
    '@type'?: Arrayable<'Dataset'>;
    /**
     * The name of the dataset.
     * This is a required field for valid Dataset structured data.
     */
    'name': string;
    /**
     * A short summary describing the dataset.
     * This is a required field for valid Dataset structured data.
     */
    'description': string;
    /**
     * The location of a page describing the dataset.
     */
    'url'?: string;
    /**
     * Keywords or tags used to describe the dataset.
     * Multiple entries in a keywords list are delimited by commas.
     */
    'keywords'?: Arrayable<string>;
    /**
     * The creator or author of this dataset.
     * Can be a Person or Organization, or a reference by ID.
     */
    'creator'?: NodeRelations<Identity>;
    /**
     * Identifies academic articles that are recommended by the data provider.
     * Can be the article text, URL, or DOI.
     */
    'citation'?: Arrayable<string>;
    /**
     * A license document that applies to this content, typically indicated by URL.
     * Can also be the license text.
     */
    'license'?: string;
    /**
     * The time period that the dataset covers, in ISO 8601 format.
     * Examples:
     * - Single date: "2008"
     * - Time period: "2007-03-01T13:00:00Z/2008-05-11T15:30:00Z"
     * - Open-ended: "2007-03-01T13:00:00Z/.."
     */
    'temporalCoverage'?: string;
    /**
     * The geographic area covered by the dataset.
     * Can be a place name, coordinates, or a shape.
     */
    'spatialCoverage'?: Arrayable<string | Thing>;
    /**
     * A download location for the dataset or a DataDownload object with distribution information.
     */
    'distribution'?: NodeRelations<DataDownload>;
    /**
     * The variables that are measured in the dataset.
     * Can be text descriptions or PropertyValue objects.
     */
    'variableMeasured'?: Arrayable<string | Thing>;
    /**
     * A data catalog which contains this dataset.
     */
    'includedInDataCatalog'?: NodeRelation<DataCatalog>;
    /**
     * Indicates whether the dataset is accessible for free.
     */
    'isAccessibleForFree'?: boolean;
    /**
     * The date on which the dataset was published, in ISO 8601 format.
     */
    'datePublished'?: ResolvableDate;
    /**
     * The date on which the dataset was most recently modified, in ISO 8601 format.
     */
    'dateModified'?: ResolvableDate;
    /**
     * The version number or identifier for this dataset.
     */
    'version'?: string;
    /**
     * A link to the license document or terms of use.
     */
    'sameAs'?: Arrayable<string>;
    /**
     * An identifier for the dataset, such as a DOI.
     */
    'identifier'?: Arrayable<string>;
}
interface Dataset extends DatasetSimple {
}
declare const PrimaryDatasetId = "#dataset";
/**
 * Describes a Dataset on a WebPage.
 * A dataset is a body of structured information describing some topic(s) of interest.
 */
declare const datasetResolver: SchemaOrgNodeDefinition<Dataset>;

/**
 * A collection of music tracks in album form.
 */
interface MusicAlbumSimple extends Thing {
    /**
     * The name of the music album.
     */
    name: string;
    /**
     * A description of the music album.
     */
    description?: string;
    /**
     * The artist that performed this album.
     * Can be a Person or MusicGroup reference.
     */
    byArtist?: NodeRelations<Person | string>;
    /**
     * A music recording (track) on this album.
     */
    track?: NodeRelations<string>;
    /**
     * The kind of release which this album is.
     * For example: "StudioAlbum", "LiveAlbum", "CompilationAlbum", "RemixAlbum", "SoundtrackAlbum", etc.
     */
    albumProductionType?: string;
    /**
     * The kind of release which this album is.
     * For example: "AlbumRelease", "SingleRelease", "EPRelease", "BroadcastRelease", etc.
     */
    albumReleaseType?: string;
    /**
     * The date the music album was published.
     */
    datePublished?: ResolvableDate;
    /**
     * Genre of the music album.
     */
    genre?: string | string[];
    /**
     * The number of tracks in this album.
     */
    numTracks?: number;
    /**
     * An image representing the music album (album art).
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * A URL to a page about the music album.
     */
    url?: string;
    /**
     * Annotation for the average review score assigned to the music album.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * A nested Review of the music album.
     */
    review?: NodeRelations<Review>;
}
interface MusicAlbum extends MusicAlbumSimple {
}
/**
 * Describes a music album.
 */
declare const musicAlbumResolver: SchemaOrgNodeDefinition<MusicAlbum>;

/**
 * A musical group, such as a band, an orchestra, or a choir.
 */
interface MusicGroupSimple extends Thing {
    /**
     * The name of the music group.
     */
    name: string;
    /**
     * A description of the music group.
     */
    description?: string;
    /**
     * Genre of the music group.
     */
    genre?: string | string[];
    /**
     * A member of the music group.
     */
    member?: NodeRelations<Person | string>;
    /**
     * The date the music group was founded.
     */
    foundingDate?: ResolvableDate;
    /**
     * The date the music group dissolved (if applicable).
     */
    dissolutionDate?: ResolvableDate;
    /**
     * A music album released by this group.
     */
    album?: NodeRelations<string>;
    /**
     * A music recording (track) by this group.
     */
    track?: NodeRelations<string>;
    /**
     * A URL to a page about the music group.
     */
    url?: string;
    /**
     * An image representing the music group.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * An array of URLs representing declared social/authoritative profiles of the music group
     * (e.g., a Wikipedia page, Facebook profile, or official website).
     */
    sameAs?: Arrayable<string>;
}
interface MusicGroup extends MusicGroupSimple {
}
/**
 * Describes a musical group, such as a band, an orchestra, or a choir.
 */
declare const musicGroupResolver: SchemaOrgNodeDefinition<MusicGroup>;

/**
 * A collection of music tracks in playlist form.
 */
interface MusicPlaylistSimple extends Thing {
    /**
     * The name of the music playlist.
     */
    name: string;
    /**
     * A description of the music playlist.
     */
    description?: string;
    /**
     * The number of tracks in this playlist.
     */
    numTracks?: number;
    /**
     * A music recording (track) in this playlist.
     */
    track?: NodeRelations<string>;
    /**
     * The creator/curator of the playlist.
     * Can be a Person or MusicGroup reference.
     */
    creator?: NodeRelation<Person | string>;
    /**
     * The date the music playlist was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The date the music playlist was last modified.
     */
    dateModified?: ResolvableDate;
    /**
     * A URL to a page about the music playlist.
     */
    url?: string;
    /**
     * An image representing the music playlist.
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * Annotation for the average review score assigned to the music playlist.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
}
interface MusicPlaylist extends MusicPlaylistSimple {
}
/**
 * Describes a collection of music tracks in playlist form.
 */
declare const musicPlaylistResolver: SchemaOrgNodeDefinition<MusicPlaylist>;

/**
 * A music recording (track), typically a single song.
 */
interface MusicRecordingSimple extends Thing {
    /**
     * The name of the music recording.
     */
    name: string;
    /**
     * A description of the music recording.
     */
    description?: string;
    /**
     * The duration of the music recording in ISO 8601 format (e.g., PT4M23S for 4 minutes 23 seconds).
     */
    duration?: string;
    /**
     * The artist that performed this recording.
     * Can be a Person or MusicGroup reference.
     */
    byArtist?: NodeRelations<Person | string>;
    /**
     * The album to which this recording belongs.
     */
    inAlbum?: NodeRelation<string>;
    /**
     * The playlist(s) this recording belongs to.
     */
    inPlaylist?: NodeRelations<string>;
    /**
     * The International Standard Recording Code for the recording.
     */
    isrcCode?: string;
    /**
     * The composition this recording is a performance of.
     */
    recordingOf?: NodeRelation<string>;
    /**
     * The date the music recording was published.
     */
    datePublished?: ResolvableDate;
    /**
     * Genre of the music recording.
     */
    genre?: string | string[];
    /**
     * A URL to a page about the music recording.
     */
    url?: string;
    /**
     * A URL to the audio file.
     */
    audio?: string;
    /**
     * An image representing the music recording (typically album art).
     */
    image?: NodeRelations<ImageObject | string>;
    /**
     * Annotation for the average review score assigned to the music recording.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
}
interface MusicRecording extends MusicRecordingSimple {
}
/**
 * Describes a music recording (track), typically a single song.
 */
declare const musicRecordingResolver: SchemaOrgNodeDefinition<MusicRecording>;

interface PodcastEpisodeSimple extends Thing {
    /**
     * The name of the episode.
     */
    name: string;
    /**
     * A description of the episode.
     */
    description?: string;
    /**
     * The episode number.
     */
    episodeNumber?: number | string;
    /**
     * The season that this episode is part of.
     */
    partOfSeason?: NodeRelation<any>;
    /**
     * The podcast series that this episode is part of.
     */
    partOfSeries?: NodeRelation<any>;
    /**
     * The creator/host of the episode.
     */
    author?: NodeRelations<Person | Organization | string>;
    /**
     * The date the episode was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The date the episode was uploaded.
     */
    uploadDate?: ResolvableDate;
    /**
     * The duration of the episode in ISO 8601 format (e.g., PT45M).
     */
    duration?: string;
    /**
     * The audio file URL or MediaObject for the episode.
     */
    audio?: NodeRelation<any | string>;
    /**
     * An image that represents the episode.
     */
    image?: NodeRelations<string | ImageObject>;
    /**
     * A thumbnail image for the episode.
     */
    thumbnailUrl?: string;
    /**
     * The URL of the episode.
     */
    url?: string;
    /**
     * A URL to a transcript of the episode.
     */
    transcript?: string;
    /**
     * Annotation for the average review score assigned to the episode.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * A nested Review of the episode.
     */
    review?: NodeRelations<Review>;
    /**
     * The language code for the episode content; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * Keywords or tags used to describe the episode.
     */
    keywords?: Arrayable<string>;
}
interface PodcastEpisode extends PodcastEpisodeSimple {
}
/**
 * Describes an episode of a podcast.
 */
declare const podcastEpisodeResolver: SchemaOrgNodeDefinition<PodcastEpisode>;

interface PodcastSeasonSimple extends Thing {
    /**
     * The name of the podcast season.
     */
    name?: string;
    /**
     * A description of the podcast season.
     */
    description?: string;
    /**
     * The season number.
     */
    seasonNumber?: number;
    /**
     * The number of episodes in the season.
     */
    numberOfEpisodes?: number;
    /**
     * The podcast series that this season is part of.
     */
    partOfSeries?: NodeRelation<any>;
    /**
     * The episodes that are part of this season.
     */
    episode?: NodeRelations<any>;
    /**
     * The date the season was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The start date of the season.
     */
    startDate?: ResolvableDate;
    /**
     * The end date of the season.
     */
    endDate?: ResolvableDate;
    /**
     * An image that represents the season.
     */
    image?: NodeRelations<string | ImageObject>;
    /**
     * The URL of the season.
     */
    url?: string;
    /**
     * The actors in the podcast season.
     */
    actor?: NodeRelations<Person | string>;
    /**
     * The directors of the podcast season.
     */
    director?: NodeRelations<Person | string>;
    /**
     * The production company or studio responsible for the podcast season.
     */
    productionCompany?: NodeRelation<Organization | string>;
    /**
     * Annotation for the average review score assigned to the podcast season.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
}
interface PodcastSeason extends PodcastSeasonSimple {
}
/**
 * Describes a season of a podcast series.
 */
declare const podcastSeasonResolver: SchemaOrgNodeDefinition<PodcastSeason>;

interface PodcastSeriesSimple extends Thing {
    /**
     * The name of the podcast.
     */
    name: string;
    /**
     * A description of the podcast.
     */
    description?: string;
    /**
     * An image that represents the podcast.
     */
    image?: NodeRelations<string | ImageObject>;
    /**
     * The URL of the podcast.
     */
    url?: string;
    /**
     * The author/creator of the podcast.
     */
    author?: NodeRelations<Person | Organization | string>;
    /**
     * The URL of the podcast RSS feed.
     */
    webFeed?: string;
    /**
     * The episodes that are part of this podcast series.
     */
    episode?: NodeRelations<any>;
    /**
     * The seasons that are part of this podcast series.
     */
    containsSeason?: NodeRelations<any>;
    /**
     * The number of episodes in the podcast series.
     */
    numberOfEpisodes?: number;
    /**
     * The number of seasons in the podcast series.
     */
    numberOfSeasons?: number;
    /**
     * The genre of the podcast.
     */
    genre?: string | string[];
    /**
     * The date the podcast was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The start date of the podcast.
     */
    startDate?: ResolvableDate;
    /**
     * The end date of the podcast (if no longer active).
     */
    endDate?: ResolvableDate;
    /**
     * Annotation for the average review score assigned to the podcast.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * The language code for the podcast content; e.g., en-GB.
     */
    inLanguage?: string;
    /**
     * Keywords or tags used to describe the podcast.
     */
    keywords?: Arrayable<string>;
}
interface PodcastSeries extends PodcastSeriesSimple {
}
/**
 * Describes a podcast series.
 */
declare const podcastSeriesResolver: SchemaOrgNodeDefinition<PodcastSeries>;

type ValidServiceSubTypes = 'Service' | 'BroadcastService' | 'CableOrSatelliteService' | 'FinancialService' | 'FoodService' | 'GovernmentService' | 'TaxiService' | 'Telecom';
/**
 * ServiceChannel defines how a service can be accessed.
 */
interface ServiceChannel {
    /**
     * The type should be ServiceChannel.
     */
    '@type'?: 'ServiceChannel';
    /**
     * The URL where the service is available.
     */
    'serviceUrl'?: string;
    /**
     * The phone number to access the service.
     */
    'servicePhone'?: string;
    /**
     * The physical location where the service is available.
     */
    'serviceLocation'?: string;
    /**
     * The languages supported by the service.
     */
    'availableLanguage'?: string | string[];
}
/**
 * A service provided by an organization, e.g. delivery service, print services, etc.
 */
interface ServiceSimple extends Thing {
    /**
     * The type of the service. Can be 'Service' or a more specific subtype.
     */
    '@type'?: Arrayable<ValidServiceSubTypes>;
    /**
     * The name of the service.
     */
    'name': string;
    /**
     * A description of the service.
     */
    'description'?: string;
    /**
     * The type of service being offered, e.g. veterans' benefits, emergency relief, etc.
     */
    'serviceType'?: string;
    /**
     * A reference to the Person or Organization that provides the service.
     */
    'provider'?: NodeRelation<Person | Organization>;
    /**
     * The geographic area where the service is provided.
     * Can be a text description or a Place object.
     */
    'areaServed'?: string | unknown;
    /**
     * A means of accessing the service (e.g. a phone bank, a web site, a location, etc.).
     */
    'availableChannel'?: ServiceChannel | ServiceChannel[];
    /**
     * An intended audience, i.e. a group for whom the service was created.
     */
    'audience'?: unknown;
    /**
     * A category for the item. Greater signs or slashes can be used to informally indicate a category hierarchy.
     */
    'category'?: string | string[];
    /**
     * Indicates an OfferCatalog listing for this Service.
     */
    'hasOfferCatalog'?: unknown;
    /**
     * An offer to provide this service—for example, an offer to perform a service for a price, or without charge.
     */
    'offers'?: NodeRelations<Offer>;
    /**
     * The overall rating, based on a collection of reviews or ratings, of the service.
     */
    'aggregateRating'?: NodeRelation<AggregateRating>;
    /**
     * A review of the service.
     */
    'review'?: NodeRelations<Review>;
    /**
     * An image of the service.
     * - Must be at least 696 pixels wide.
     * - Must be of the following formats+file extensions: .jpg, .png, .gif, or .webp.
     */
    'image'?: NodeRelations<ImageObject | string>;
    /**
     * A logo associated with the service.
     */
    'logo'?: NodeRelations<ImageObject | string>;
    /**
     * URL of the service.
     */
    'url'?: string;
    /**
     * Human-readable terms of service documentation.
     */
    'termsOfService'?: string;
    /**
     * A slogan or motto associated with the service.
     */
    'slogan'?: string;
    /**
     * The brand associated with the service.
     */
    'brand'?: NodeRelation<Organization>;
}
interface Service extends ServiceSimple {
}
declare const ServiceId = "#service";
/**
 * Describes a service provided by an organization or person.
 */
declare const serviceResolver: SchemaOrgNodeDefinition<Service>;

interface TVEpisodeSimple extends Thing {
    /**
     * The name of the episode.
     */
    name: string;
    /**
     * A description of the episode.
     */
    description?: string;
    /**
     * The episode number.
     */
    episodeNumber?: number | string;
    /**
     * The season that this episode is part of.
     */
    partOfSeason?: NodeRelation<any>;
    /**
     * The TV series that this episode is part of.
     */
    partOfSeries?: NodeRelation<any>;
    /**
     * The actors in the episode.
     */
    actor?: NodeRelations<Person | string>;
    /**
     * The directors of the episode.
     */
    director?: NodeRelations<Person | string>;
    /**
     * The date the episode was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The date the episode was uploaded.
     */
    uploadDate?: ResolvableDate;
    /**
     * The duration of the episode in ISO 8601 format (e.g., PT45M).
     */
    duration?: string;
    /**
     * A video object representing the episode content.
     */
    video?: NodeRelation<VideoObject | string>;
    /**
     * An image that represents the episode.
     */
    image?: NodeRelations<string | ImageObject>;
    /**
     * A thumbnail image for the episode.
     */
    thumbnailUrl?: string;
    /**
     * The URL of the episode.
     */
    url?: string;
    /**
     * Annotation for the average review score assigned to the episode.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * A nested Review of the episode.
     */
    review?: NodeRelations<Review>;
    /**
     * Official rating of the content (e.g., "MPAA PG-13", "TV-MA").
     */
    contentRating?: string;
    /**
     * The composer of the episode's musical score.
     */
    musicBy?: NodeRelations<Person | string>;
}
interface TVEpisode extends TVEpisodeSimple {
}
/**
 * Describes an episode of a TV series.
 */
declare const tvEpisodeResolver: SchemaOrgNodeDefinition<TVEpisode>;

interface TVSeasonSimple extends Thing {
    /**
     * The name of the TV season.
     */
    name?: string;
    /**
     * A description of the TV season.
     */
    description?: string;
    /**
     * The season number.
     */
    seasonNumber?: number;
    /**
     * The number of episodes in the season.
     */
    numberOfEpisodes?: number;
    /**
     * The TV series that this season is part of.
     */
    partOfSeries?: NodeRelation<any>;
    /**
     * The episodes that are part of this season.
     */
    episode?: NodeRelations<any>;
    /**
     * The date the season was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The start date of the season.
     */
    startDate?: ResolvableDate;
    /**
     * The end date of the season.
     */
    endDate?: ResolvableDate;
    /**
     * An image that represents the season.
     */
    image?: NodeRelations<string | ImageObject>;
    /**
     * The URL of the season.
     */
    url?: string;
    /**
     * The actors in the TV season.
     */
    actor?: NodeRelations<Person | string>;
    /**
     * The directors of the TV season.
     */
    director?: NodeRelations<Person | string>;
    /**
     * The production company or studio responsible for the TV season.
     */
    productionCompany?: NodeRelation<Organization | string>;
    /**
     * Annotation for the average review score assigned to the TV season.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * Official rating of the content (e.g., "MPAA PG-13", "TV-MA").
     */
    contentRating?: string;
    /**
     * A trailer or preview video for the TV season.
     */
    trailer?: NodeRelation<VideoObject | string>;
}
interface TVSeason extends TVSeasonSimple {
}
/**
 * Describes a season of a TV series.
 */
declare const tvSeasonResolver: SchemaOrgNodeDefinition<TVSeason>;

interface TVSeriesSimple extends Thing {
    /**
     * The name of the TV series.
     */
    name: string;
    /**
     * A description of the TV series.
     */
    description?: string;
    /**
     * An image that represents the TV series.
     */
    image?: NodeRelations<string | ImageObject>;
    /**
     * The URL of the TV series.
     */
    url?: string;
    /**
     * The actors in the TV series.
     */
    actor?: NodeRelations<Person | string>;
    /**
     * The directors of the TV series.
     */
    director?: NodeRelations<Person | string>;
    /**
     * The creator of the TV series.
     */
    creator?: NodeRelations<Person | Organization | string>;
    /**
     * The number of seasons in the TV series.
     */
    numberOfSeasons?: number;
    /**
     * The number of episodes in the TV series.
     */
    numberOfEpisodes?: number;
    /**
     * The seasons that are part of this TV series.
     */
    containsSeason?: NodeRelations<any>;
    /**
     * The episodes that are part of this TV series.
     */
    episode?: NodeRelations<any>;
    /**
     * The genre of the TV series.
     */
    genre?: string | string[];
    /**
     * The date the TV series was published.
     */
    datePublished?: ResolvableDate;
    /**
     * The start date of the TV series.
     */
    startDate?: ResolvableDate;
    /**
     * The end date of the TV series.
     */
    endDate?: ResolvableDate;
    /**
     * The production company or studio responsible for the TV series.
     */
    productionCompany?: NodeRelation<Organization | string>;
    /**
     * Annotation for the average review score assigned to the TV series.
     */
    aggregateRating?: NodeRelation<AggregateRating>;
    /**
     * The country of origin for the TV series.
     */
    countryOfOrigin?: string;
    /**
     * A trailer or preview video for the TV series.
     */
    trailer?: NodeRelation<VideoObject | string>;
    /**
     * Official rating of the content (e.g., "MPAA PG-13", "TV-MA").
     */
    contentRating?: string;
}
interface TVSeries extends TVSeriesSimple {
}
/**
 * Describes a TV series.
 */
declare const tvSeriesResolver: SchemaOrgNodeDefinition<TVSeries>;

declare function defineAddress<T extends Record<string, any>>(input?: PostalAddress & T): (PostalAddressStrict & T) | (PostalAddressName & T);
declare function defineAggregateOffer<T extends Record<string, any>>(input?: AggregateOffer & T): AggregateOffer & T;
declare function defineAggregateRating<T extends Record<string, any>>(input?: AggregateRating & T): AggregateRating & T;
declare function defineArticle<T extends Record<string, any>>(input?: Article & T): Article & T;
declare function defineBreadcrumb<T extends Record<string, any>>(input?: BreadcrumbList & T): BreadcrumbList & T;
declare function defineComment<T extends Record<string, any>>(input?: Comment & T): Comment & T;
declare function defineEvent<T extends Record<string, any>>(input?: Event & T): Event & T;
declare function defineFoodEstablishment<T extends Record<string, any>>(input?: FoodEstablishment & T): FoodEstablishment & T;
declare function defineVirtualLocation<T extends Record<string, any>>(input?: VirtualLocation & T): VirtualLocation & T;
declare function definePlace<T extends Record<string, any>>(input?: Place & T): Place & T;
declare function defineHowTo<T extends Record<string, any>>(input?: HowTo & T): HowTo & T;
declare function defineHowToStep<T extends Record<string, any>>(input?: HowToStep & T): HowToStep & T;
declare function defineImage<T extends Record<string, any>>(input?: ImageObject & T): ImageObject & T;
declare function defineJobPosting<T extends Record<string, any>>(input?: JobPosting & T): JobPosting & T;
declare function defineLocalBusiness<T extends Record<string, any>>(input?: LocalBusiness & T): LocalBusiness & T;
declare function defineOffer<T extends Record<string, any>>(input?: Offer & T): Offer & T;
declare function defineOpeningHours<T extends Record<string, any>>(input?: OpeningHoursSpecification & T): OpeningHoursSpecification & T;
declare function defineOrganization<T extends Record<string, any>>(input?: Organization & T): Organization & T;
declare function definePerson<T extends Record<string, any>>(input?: Person & T): Person & T;
declare function defineProduct<T extends Record<string, any>>(input?: Product & T): Product & T;
declare function defineQuestion<T extends Record<string, any>>(input?: Question & T): Question & T;
declare function defineRecipe<T extends Record<string, any>>(input?: Recipe & T): Recipe & T;
declare function defineReview<T extends Record<string, any>>(input?: Review & T): Review & T;
declare function defineVideo<T extends Record<string, any>>(input?: VideoObject & T): VideoObject & T;
declare function defineWebPage<T extends Record<string, any>>(input?: WebPage & T): WebPage & T;
declare function defineWebSite<T extends Record<string, any>>(input?: WebSite & T): WebSite & T;
declare function defineBook<T extends Record<string, any>>(input?: Book & T): Book & T;
declare function defineCourse<T extends Record<string, any>>(input?: Course & T): Course & T;
declare function defineItemList<T extends Record<string, any>>(input?: ItemList & T): ItemList & T;
declare function defineListItem<T extends Record<string, any>>(input?: ListItem & T): ListItem & T;
declare function defineMovie<T extends Record<string, any>>(input?: Movie & T): Movie & T;
declare function defineSearchAction<T extends Record<string, any>>(input?: SearchAction & T): SearchAction & T;
declare function defineReadAction<T extends Record<string, any>>(input?: ReadAction & T): ReadAction & T;
declare function defineDataset<T extends Record<string, any>>(input?: Dataset & T): Dataset & T;
declare function defineMusicRecording<T extends Record<string, any>>(input?: MusicRecording & T): MusicRecording & T;
declare function defineMusicAlbum<T extends Record<string, any>>(input?: MusicAlbum & T): MusicAlbum & T;
declare function defineMusicGroup<T extends Record<string, any>>(input?: MusicGroup & T): MusicGroup & T;
declare function defineMusicPlaylist<T extends Record<string, any>>(input?: MusicPlaylist & T): MusicPlaylist & T;
declare function definePodcastSeries<T extends Record<string, any>>(input?: PodcastSeries & T): PodcastSeries & T;
declare function definePodcastEpisode<T extends Record<string, any>>(input?: PodcastEpisode & T): PodcastEpisode & T;
declare function definePodcastSeason<T extends Record<string, any>>(input?: PodcastSeason & T): PodcastSeason & T;
declare function defineTVSeries<T extends Record<string, any>>(input?: TVSeries & T): TVSeries & T;
declare function defineTVSeason<T extends Record<string, any>>(input?: TVSeason & T): TVSeason & T;
declare function defineTVEpisode<T extends Record<string, any>>(input?: TVEpisode & T): TVEpisode & T;
declare function defineService<T extends Record<string, any>>(input?: Service & T): Service & T;
declare function defineSoftwareApp<T extends Record<string, any>>(input?: SoftwareApp & T): SoftwareApp & T;
declare function defineBookEdition<T extends Record<string, any>>(input?: BookEdition & T): BookEdition & T;
type UseSchemaOrgInput = Arrayable<Thing | Record<string, any>>;
declare function normalizeSchemaOrgInput<T extends UseSchemaOrgInput>(input: T): T;
declare function useSchemaOrg(unhead: Unhead<any>, input?: UseSchemaOrgInput, options?: HeadEntryOptions): ActiveHeadEntry<UseSchemaOrgInput>;

export { defineOrganization as A, definePerson as B, definePlace as C, definePodcastEpisode as D, definePodcastSeason as E, definePodcastSeries as F, defineProduct as G, defineQuestion as H, defineReadAction as I, defineRecipe as J, defineReview as K, defineSearchAction as L, defineService as M, defineSoftwareApp as N, defineTVEpisode as O, defineTVSeason as P, defineTVSeries as Q, defineVideo as R, defineVirtualLocation as S, defineWebPage as T, defineWebSite as U, normalizeSchemaOrgInput as V, useSchemaOrg as W, defineAggregateOffer as a, PrimaryDatasetId as a0, datasetResolver as a1, musicAlbumResolver as a4, musicGroupResolver as a7, tvSeriesResolver as aA, musicPlaylistResolver as aa, musicRecordingResolver as ad, podcastEpisodeResolver as ag, podcastSeasonResolver as aj, podcastSeriesResolver as am, ServiceId as aq, serviceResolver as ar, tvEpisodeResolver as au, tvSeasonResolver as ax, defineAggregateRating as b, defineArticle as c, defineAddress as d, defineBook as e, defineBookEdition as f, defineBreadcrumb as g, defineComment as h, defineCourse as i, defineDataset as j, defineEvent as k, defineFoodEstablishment as l, defineHowTo as m, defineHowToStep as n, defineImage as o, defineItemList as p, defineJobPosting as q, defineListItem as r, defineLocalBusiness as s, defineMovie as t, defineMusicAlbum as u, defineMusicGroup as v, defineMusicPlaylist as w, defineMusicRecording as x, defineOffer as y, defineOpeningHours as z };
export type { Dataset as $, UseSchemaOrgInput as X, DataDownload as Y, DataCatalog as Z, DatasetSimple as _, MusicAlbumSimple as a2, MusicAlbum as a3, MusicGroupSimple as a5, MusicGroup as a6, MusicPlaylistSimple as a8, MusicPlaylist as a9, MusicRecordingSimple as ab, MusicRecording as ac, PodcastEpisodeSimple as ae, PodcastEpisode as af, PodcastSeasonSimple as ah, PodcastSeason as ai, PodcastSeriesSimple as ak, PodcastSeries as al, ServiceChannel as an, ServiceSimple as ao, Service as ap, TVEpisodeSimple as as, TVEpisode as at, TVSeasonSimple as av, TVSeason as aw, TVSeriesSimple as ay, TVSeries as az };
